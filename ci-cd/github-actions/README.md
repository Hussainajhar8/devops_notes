# GitHub Actions

GitHub Actions is a tool designed to automate software development workflows. Workflows are configurable automated processes that perform various tasks such as testing, publishing a package, deploying applications, notifying users, and opening issues. A workflow can consist of multiple jobs, and each job can have a series of steps. [Refer To Documentation when creating pipelines](https://docs.github.com/en/actions)

## Table of Contents

- [GitHub Actions](#github-actions)
  - [Table of Contents](#table-of-contents)
- [Section 1: Intro \& Basic Concepts](#section-1-intro--basic-concepts)
- [Section 2: Events that Trigger Workflows](#section-2-events-that-trigger-workflows)
- [Section 3: Expressions, Contexts, Functions, Environment Variables \& Secrets](#section-3-expressions-contexts-functions-environment-variables--secrets)
- [Section 4: Diving Deeper with More Advanced GitHub Actions Features](#section-4-diving-deeper-with-more-advanced-github-actions-features)
- [Section 5: Using Docker in GitHub Actions](#section-5-using-docker-in-github-actions)


# Section 1: Intro & Basic Concepts

**Key Components of GitHub Actions:**

- **Workflows:** Workflows are triggered by events and define the automated processes to be executed. They can contain multiple jobs, each with its own set of steps.
  
- **Events:** Events trigger workflows. These events can include push events, pull request events, issue events, scheduled events, and more.
  
- **Jobs:** Jobs are the individual units of work within a workflow. They can run in parallel or sequentially, depending on the configuration.
  
- **Steps:** Steps are the individual tasks that make up a job. They can include commands, actions, and the execution of Docker containers.
  
- **Actions:** Actions are custom applications that perform complex but frequently repeated tasks. They can be used within workflows to automate various processes.

![alt text](img/image.png)
  
- **YAML:** Workflows are written in YAML (YAML Ain't Markup Language), a human-readable data serialization format. YAML files define the structure of workflows, including events, jobs, and steps. Here's a quick [YAML reference](https://learnxinyminutes.com/docs/yaml/) for more information.

GitHub Actions provides a flexible and powerful platform for automating software development workflows, helping teams streamline their development processes and improve productivity.

**Creating a Workflow**

Workflows in GitHub Actions must be created in the `.github/workflows/` directory. A workflow file should include the following components:

- **Name:** A descriptive name for the workflow.
- **On:** An event trigger that specifies when the workflow should be executed.
- **Jobs:** The main section of the workflow file, containing the steps to be executed.
  <br>![alt text](img/image-1.png)

1. **Parallel Jobs and Dependencies:**

Jobs can be configured to run in parallel by simply adding additional job definitions to the workflow file. To run a job as a dependent job, you need to use the `needs` block to specify dependencies between jobs.
<br>![alt text](img/image-2.png)
<br>![alt text](img/image-3.png)

2. **Disabling Workflows:**

You can disable a workflow on GitHub to prevent it from running at all. This can be useful when you need to temporarily suspend a workflow.
<br>![alt text](img/image-4.png)
<br>![alt text](img/image-5.png)
after clicking on a workflow, you have an option to re-run all or the failed jobs, you can also cancel a job whilst it is running.
<br>![alt text](img/image-6.png)

3. **Debugging:**

GitHub Actions provides several debugging features:
- Searching and downloading logs.
- Clicking on the line of an error to generate a URL that directly links to the error line.
- Enabling debug logging by setting specific environment variables (`ACTIONS_STEP_DEBUG=true` and `ACTIONS_RUNNER_DEBUG=true`).
  <br>![alt text](img/image-7.png)
  <br>![alt text](img/image-8.png)

You can also skip a workflow by including specific keywords in square brackets in the commit message which are [ skip ci, ci skip, no ci, skip actions, actions skip ].
<br>![alt text](img/image-9.png)

4. **Workflow Commands:**

You can use workflow commands to display messages, group logs, and mask sensitive information. Here are some examples:
- Displaying an error message: `echo "::error::<error-message-you-want-to-display>"`
  <br>![alt text](img/image-10.png)
- Displaying debug, notice, and warning messages with the similar conventation as error.
  <br>![alt text](img/image-11.png)
- Grouping logs with `::group::` and `::endgroup::`.
  <br>![alt text](img/image-12.png)
- Masking variables with `::add-mask::<variable_name>` to prevent them from being displayed in standard output.
  <br>![alt text](img/image-13.png)

5. **Shells and Working Directory:**

- You can set the default shell for all jobs by `defaults: run: shell: bash` at the top of the workflow file, you can also do this for working directory default `defaults: run: working-directory: /set_the_workding_directory_path/`
<br>![alt text](img/image-14.png)<br>
- Additionally, you can override defaults at the job level,
<br>![alt text](img/image-15.png)<br>
- and step level.<br>
<br>![alt text](img/image-16.png)

6. **Downloading Repositories into Runner Machines:**

- Manually downloading repositories into runner machines can be done using a specific workflow configuration. 
<br>![alt text](img/image-17.png)
- However, it's much simpler to achieve this using actions, which are reusable units of code. 
  <br>![alt text](img/image-18.png)
- Actions can be referenced using the `uses` syntax, and you can reference the output of an action by setting an `id` for the action step and referencing it with `${{ steps.<id>.outputs.<output_name> }}`.
- <br>![alt text](img/image-19.png)

# Section 2: Events that Trigger Workflows

1. **Repository Events:** 
   - Events can be configured using the `on` block, with options such as `[push, pull_requests, issues]`.
   - You can specify the activity type with `types` after the event, determining which activity of that event will trigger the workflow.
     <br>![alt text](img/image-20.png)
   - For forked pull requests, workflows can be approved. In private repositories, enable workflow fork pull requests in repo settings under `Settings` > `Actions` <br> 
    <br>![alt text](img/image-21.png),
    <br> and specify who needs approval in GitHub repo settings.
    <br>![alt text](img/image-22.png)

2. Use `pull_request_target` event to run in the context of the base of the pull request rather than in the context of the merge commit. This allows actions like labeling or commenting on pull requests from forks. Avoid using this event if you need to build or run code from the pull request.

3. Trigger another workflow with `workflow_run`, useful for running dependent workflows. Specify the workflows to trigger under `workflows: [<name of workflow1>, <name of workflow2>]`.
   <br>![alt text](img/image-23.png)

4. Filter workflow runs on specific branches, tags, and paths by adding `branches` and specifying branches. Note: the order is important, and if you want to exclude a branch, it should be placed at the end. All filters set must be matched for the workflow to run.
   <br>![alt text](img/image-24.png)

5. Use the Workflow Dispatch event to enable manual triggering, displaying a button on GitHub for manual triggering of the workflow.
   <br>![alt text](img/image-25.png)
   - Inputs can be added to the workflow, containing a name, description, type, and default value. 
   <br>![alt text](img/image-26.png)
   - They can be referenced in the workflow with `{{ inputs.<name_of_input> }}`.
     <br>![alt text](img/image-27.png)
   - Triggered with `gh cli` using `gh workflow run`, and via the GitHub REST API using fine-grained access token and curl commands.
    <br>![alt text](img/image-28.png)

6. `repository_dispatch` can be used to trigger workflows based on external events such as a webhook.
   <br>![alt text](img/image-29.png)

7. Events can be scheduled to run at specified intervals, such as daily, every 10 minutes, or every hour.
   <br>![alt text](img/image-30.png)

# Section 3: Expressions, Contexts, Functions, Environment Variables & Secrets

1. **Expressions**:
   - Expressions are used to programmatically set environment variables in workflow files and access contexts. They can be any combination of literal values, references to a context, or functions. Expressions are in the format `${{ <value> }}`.

2. **Contexts**:
   - Contexts provide information about workflow runs, variables, runner environments, jobs, and steps. Each context is an object containing properties, which can be strings or other objects. They're accessed using the expression syntax `${{ <context> }}`.
  <br>![alt text](img/image-31.png)

3. **Conditional Clauses**:
   - Workflows can use conditional clauses like `if`.
     <br>![alt text](img/image-32.png)
     - `contains(search, item)`: Returns true if `search` contains `item`. If `search` is an array, it returns true if `item` is an element in the array. If `search` is a string, it returns true if `item` is a substring of `search`. This function is not case-sensitive and casts values to a string.
      <br>![alt text](img/image-33.png)
     - The `*` syntax applies a filter to select matching items in a collection.
       For example, consider an array of objects named fruits.<br>
       <br>![alt text](img/image-34.png)<br>
       The filter fruits.*.name returns the array [ "apple", "orange", "pear" ].


4. **Status Check Functions**:
   - These functions are used as expressions in `if` conditionals and include `[success, always, cancelled, failure]` with conditions.

5. **Default Environment Variables**:
   - A list of default variables can be found in the [documentation](https://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables).
     - In `if` conditionals, use the context and not environment variables because the conditional is processed by GitHub Actions before the workflow runs on the runner machine so any environment variables from the runner machine won’t work here.
       <br>![alt text](img/image-35.png)
     - custom environment variables can be configured with `env:` on three levels: workflow, job and step - depending on where you place the `env:` in the workflow file, the env set in lower levels override those above it.


6. **Setting Environment Variables**:
   - During workflow execution, environment variables can be set by running `echo "{environment_variable_name}={value}" >> "$GITHUB_ENV"`.
    <br>![alt text](img/image-36.png)
     - For multiline strings, use a delimiter.
     - Syntax is like this:
      <br>![alt text](img/image-37.png)
     - An example will look like this:
      <br>![alt text](img/image-38.png)
      And the output is this.
      <br>![alt text](img/image-39.png)
    - Note: the delimiter should be unique and uncommon so that it doesn’t accidently get fetched in the content of the value and end up giving an incomplete value because it wasn’t parsed properly

7. **Configuration Variables**:
   - These variables can be used to set secrets/variables at the repo or organization level. They can be configured on the GitHub UI, and environments will override those above them (environment > repo > organization).
    <br>![alt text](img/image-40.png)

8. **Secrets**:
   - Secrets are limited to 48KB. For larger secrets, save the encrypted file to the repository, set a passphrase to decrypt the file as a secret, and use it when running a command to decrypt the file.
    <br>![alt text](img/image-41.png)

9. **Default GITHUB_TOKEN Secret**:
   - By default, GitHub Actions uses a randomly generated `GITHUB_TOKEN` secret authentication token for the duration of the workflow on the runner machine. However, it's recommended to edit permissions in your workflow to only give the permissions needed for the workflow to run.
    <br>![alt text](img/image-42.png)

# Section 4: Diving Deeper with More Advanced GitHub Actions Features

1. **Continue-on-Error and Timeout**:
   - Set `continue-on-error` to allow the workflow to continue even if a step fails.
    <br>![alt text](img/image-43.png) <br>![alt text](img/image-44.png)
   - Use `timeout-minutes` to specify the maximum duration a step can run before it returns an error. Setting this at the job level will cancel the job if it times out.

2. **Matrix Jobs**:
   - Run jobs multiple times with different parameters using a matrix strategy. Configure this with the `strategy` key, followed by `matrix` and the names of your matrices.
    <br>![alt text](img/image-45.png)
   - Create multi-dimensional matrices by adding more arrays.
    <br>![alt text](img/image-46.png)
   - Further configure with `max-parallel` (maximum parallel jobs), `continue-on-error` (continue workflow if a job fails), and `fail-fast: false` (continue other jobs if one fails).
    <br>![alt text](img/image-47.png)
   - Use `include` and `exclude` to specify matrix configurations.
    <br>![alt text](img/image-48.png)
   - Set outputs in a run step: 
     `run: echo “<name_of_output>=<value_you_want_to_set>” >> $GITHUB_OUTPUT`
     Access later with `steps.<id_of_step>.outputs.<name_of_output>`.
     <br>![alt text](img/image-49.png)
   - Use actions like `actions/github-script@v6` to easily create outputs using the GitHub API and workflow context by writing scripts.
    <br>![alt text](img/image-50.png)
   - Set job-level outputs with `outputs:` to make step outputs available for the entire job.
    <br>![alt text](img/image-51.png)
   - Convert strings to arrays using `client_payload` to pass arrays outside of manual workflows (the steps before is for `workflow_dispatch` which is manual approval).
    <br>![alt text](img/image-52.png)

3. **Concurrency**:
   - Use `concurrency:` and `group: <name_of_group>` to create concurrency groups where jobs run one at a time.
   - Set `cancel-in-progress: true` to cancel running jobs and only run the latest one in the group.
   - Isolate concurrent jobs by their environment with `group: ${{ github.event.inputs.environment }}`.
    <br>![alt text](img/image-53.png)

4. **Reusable Workflows**:
   - Reusable workflows can be in the same or different repositories.
   - Define reusable workflows events with `workflow_call` and `inputs`.
   - Ensure the repository/organization allows reusable workflows.
   - Access reusable workflow outputs with `needs.<name_of_reusable_workflow>.outputs.<output_name>`.
    <br>![alt text](img/image-54.png)
   - Use `secrets: inherit` to pass secrets to reusable workflows.
    <br>![alt text](img/image-55.png)

5. **Caching Files in GitHub Actions**:
   - Use cache actions to cache files. Set `key` and `path` to store the cache. Use the same key to access the cache in future workflows.
   - Use dynamic keys to handle changes in the environment or dependencies, e.g., `key: ${{ runner.os }}-npm-cache-${{ hashFiles('**/package-lock.json') }}`. This is useful to create a new and updated cache, it will print a key name like ‘linux-npm-cache-7383493’
   - Restore older caches with shorthand keys if the specified cache is not found.
    <br>![alt text](img/image-57.png)
   - Find caches in the GitHub Actions cache section.
   - Some actions, like `setup-node`, handle their own caching.
    <br>![alt text](img/image-58.png)
   - Unused caches are deleted after 7 days and are limited to 10GB per repository.
   - The main branch can't access caches from feature branches and pull request caches are only available to that branch.
    <br>![alt text](img/image-59.png)
   - Use workflows to clean up caches, removing unneeded PR caches while retaining important ones. See more [here](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows).
   - Save files produced by a job as artifacts using `actions/upload-artifact` and `actions/download-artifact`. Set `path` and `retention-days`.

# Section 5: Using Docker in GitHub Actions

1. **Running Jobs in Docker Containers**
   - Specify `container` as an option inside the job with its `image`.
   - If the image is private, specify `credentials`.
   - Set environment variables with `env`, `ports`, and `volumes` for named volumes, anonymous volumes, and bind mounts.
   - Use `options` to specify additional docker command options.
<br>![alt text](img/image-60.png)

2. **Running Docker Containers on the Step Level**
   - Specify the image in the `uses` option instead of an action.
   - Set the `entrypoint` and `args` within the `with` key.
<br>![alt text](img/image-61.png)

3. **Docker Containers on the Same Machine**
   - Containers on the same machine use the same network and volumes, allowing files to be accessed by different containers.

4. **Passing a Script to a Container**
   - Set the script path in the `entrypoint` option in a container. Ensure the script has the correct execute permissions.

5. **Using Service Containers in Jobs**
   - Add the `services` option and a name for the app, then configure it with `image`, `ports`, and `env`.
   - Steps will run on the runner machine, but applications will be available on `localhost` at specified ports and also on the `name:port` of the container. 
   - Docker exposes all ports to containers within the same network.
<br>![alt text](img/image-62.png)
6. **Publishing Docker Images with GitHub Actions**
   - Use Docker's login action and build and push action to publish Docker images.
