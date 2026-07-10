# Episode 1 Scenario Questions and Answers

## 1. Your workflow does not start after a push to `main`. What do you check first?

Check the trigger branch, the workflow file path, and the event type. A workflow that never starts usually has a trigger mismatch rather than a runner problem.

## 2. The job starts, but the commands seem too small to prove anything. Why begin here?

Because the point of the first episode is to confirm that GitHub Actions can actually run the workflow before we add build, test, or deploy complexity.

## 3. A teammate asks what a workflow, job, and step are. How do you explain them in this pipeline?

A workflow is the automation file, a job is one execution unit inside it, and a step is one command or action inside that job.

## 4. The runner succeeds, but you still do not trust the result. What signal tells you the pipeline really ran?

The file listing and echoed message show that the runner checked out the repo and executed commands in order.

## 5. You want to make the pipeline more useful without making it harder to read. What would you add next?

Add one small verification step at a time, such as printing the date or event name, so the workflow stays easy to understand while it grows.

## 6. A push works on one branch but not another. What is your first suspicion?

The branch filter or path filter is probably different from what you expected, so check the workflow trigger configuration first.

## 7. The workflow runs, but reviewers still cannot tell whether the repo contents were available. What extra signal would you add?

Add a file listing or a targeted check that proves the checkout happened and the workspace contains the expected project files.
