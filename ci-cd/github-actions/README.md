# GitHub Actions

GitHub Actions is a tool designed to automate software development workflows. Workflows are configurable automated processes that perform various tasks such as testing, publishing a package, deploying applications, notifying users, and opening issues. A workflow can consist of multiple jobs, and each job can have a series of steps.

### Key Components of GitHub Actions:

- **Workflows:** Workflows are triggered by events and define the automated processes to be executed. They can contain multiple jobs, each with its own set of steps.
  
- **Events:** Events trigger workflows. These events can include push events, pull request events, issue events, scheduled events, and more.
  
- **Jobs:** Jobs are the individual units of work within a workflow. They can run in parallel or sequentially, depending on the configuration.
  
- **Steps:** Steps are the individual tasks that make up a job. They can include commands, actions, and the execution of Docker containers.
  
- **Actions:** Actions are custom applications that perform complex but frequently repeated tasks. They can be used within workflows to automate various processes.

![alt text](img/image.png)
  
- **YAML:** Workflows are written in YAML (YAML Ain't Markup Language), a human-readable data serialization format. YAML files define the structure of workflows, including events, jobs, and steps. Here's a quick [YAML reference](https://learnxinyminutes.com/docs/yaml/) for more information.

GitHub Actions provides a flexible and powerful platform for automating software development workflows, helping teams streamline their development processes and improve productivity.

### Creating a Workflow

Workflows in GitHub Actions must be created in the `.github/workflows/` directory. A workflow file should include the following components:

- **Name:** A descriptive name for the workflow.
- **On:** An event trigger that specifies when the workflow should be executed.
- **Jobs:** The main section of the workflow file, containing the steps to be executed.
  ![alt text](img/image-1.png)

1. Parallel Jobs and Dependencies

Jobs can be configured to run in parallel by simply adding additional job definitions to the workflow file. To run a job as a dependent job, you need to use the `needs` block to specify dependencies between jobs.
![alt text](img/image-2.png)
![alt text](img/image-3.png)

2. Disabling Workflows

You can disable a workflow on GitHub to prevent it from running at all. This can be useful when you need to temporarily suspend a workflow.
![alt text](img/image-4.png)
![alt text](img/image-5.png)
after clicking on a workflow, you have an option to re-run all or the failed jobs, you can also cancel a job whilst it is running.
![alt text](img/image-6.png)

### Debugging

GitHub Actions provides several debugging features:
- Searching and downloading logs.
- Clicking on the line of an error to generate a URL that directly links to the error line.
- Enabling debug logging by setting specific environment variables (`ACTIONS_STEP_DEBUG=true` and `ACTIONS_RUNNER_DEBUG=true`).
  ![alt text](img/image-7.png)
  ![alt text](img/image-8.png)

You can also skip a workflow by including specific keywords in square brackets in the commit message which are [ skip ci, ci skip, no ci, skip actions, actions skip ].
![alt text](img/image-9.png)

### Workflow Commands

You can use workflow commands to display messages, group logs, and mask sensitive information. Here are some examples:
- Displaying an error message: `echo "::error::<error-message-you-want-to-display>"`
  ![alt text](img/image-10.png)
- Displaying debug, notice, and warning messages with the similar conventation as error.
  ![alt text](img/image-11.png)
- Grouping logs with `::group::` and `::endgroup::`.
  ![alt text](img/image-12.png)
- Masking variables with `::add-mask::<variable_name>` to prevent them from being displayed in standard output.
  ![alt text](img/image-13.png)

### Shells and Working Directory

- You can set the default shell for all jobs by `defaults: run: shell: bash` at the top of the workflow file, you can also do this for working directory default `defaults: run: working-directory: /set_the_workding_directory_path/`
![alt text](img/image-14.png)<br>
- Additionally, you can override defaults at the job level,
![alt text](img/image-15.png)<br>
- and step level.<br>
![alt text](img/image-16.png)

### Downloading Repositories into Runner Machines

- Manually downloading repositories into runner machines can be done using a specific workflow configuration. 
![alt text](img/image-17.png)
- However, it's much simpler to achieve this using actions, which are reusable units of code. 
  ![alt text](img/image-18.png)
- Actions can be referenced using the `uses` syntax, and you can reference the output of an action by setting an `id` for the action step and referencing it with `${{ steps.<id>.outputs.<output_name> }}`.
- ![alt text](img/image-19.png)
