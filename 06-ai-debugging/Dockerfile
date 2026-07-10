FROM python:3.11-slim

# Keep the image small and the runtime predictable.
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_NO_CACHE_DIR=1

WORKDIR /app

# Run the app as a non-root user, which is the safer default.
RUN useradd --create-home --uid 10001 --shell /usr/sbin/nologin appuser

# Install dependencies before copying the app so Docker can cache the layer better.
COPY requirements.txt .

# Upgrade pip, then install the pinned dependencies.
RUN python -m pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy only the application code into the image.
COPY app ./app

# Document the container port for humans and tooling.
EXPOSE 5000

# Healthcheck lets Docker confirm the app is alive inside the container.
HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:5000/healthz')" || exit 1

# Drop root before the app starts.
USER appuser

# Gunicorn is the production WSGI server used in all full-series episodes.
CMD ["gunicorn", "--chdir", "app", "--bind", "0.0.0.0:5000", "--workers", "2", "--threads", "4", "--access-logfile", "-", "--error-logfile", "-", "app:app"]
