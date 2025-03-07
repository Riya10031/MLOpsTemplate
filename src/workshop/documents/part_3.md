
# Part 3: Use GitHub for Version Control and Automation

## Pre-requisites
- Complete [Part 0], [Part 1], [Part 2]

## Summary
Your team wants to learn how to automate and orchestrate common tasks such as environment setup, training, and testing using GitHub Actions. To accomplish this, the following steps will be performed:
- Setup a centralized version control to keep track of project code and manage different feature development tracks and releases
- Learn how to automate and orchestrate common tasks such as environment setup, training, and testing by setting up a unit test workflow to run when code is updated in your branch

## Steps
1. Move to the dev branch you created in step 1 if you are not already there.
   > - Navigate to the repo if not already there ```cd MLOpsTemplate``` with the proper path to the cloned location.
    
   >**Action Items:** 

   >- If you are in the workshop folder, Run the following command to switch back files until you reach your repo i.e. MLOpsTemplate
    
   ```bash
   cd ..
   ```

   >- Run the following command to check out your "yourname-dev"
        
   ```bash
   git checkout yourname-dev
   ```

1. Create an automated unit test task that will be triggered by pushing the code to your development/feature branch. Let's use the ```Feature_Engineering``` module as the automated unit test to run to make sure the module performs correctly.

   >**Action Items:** Update the `workshop_unit_test.yml` file with your secret credentials. Replace the resource group, workspace and location with your specific details.

   >- Locate the file named `workshop_unit_test.yml` in the `.github/workflows` folder by running the following command:
    
   ```bash
   cd .github/workflows/
   nano workshop_unit_test.yml
   ```
   >- Make the following updates to the file: 
   >- Update the secret name by replacing the ```AZURE_SERVICE_PRINCIPAL``` to match the GitHub secret name for your Service Principal that was created in Part 0. (If you followed the naming convention in Part 0, there is no need to update this as your secret name should be ```AZURE_SERVICE_PRINCIPAL```.)
   >- Update the resource group name, workspace name, and location with the specific names of your resource group, workspace, and location created in Part 0.
 
   >**Note:** You can use the arrow keys to move around in the file. Press the "CTRL + X" keys to close the file. You will be prompted to save your changes. Press the "y" key to save your changes and then press enter to exit.

1. Next, review the contents in the ```workshop_unit_test.yml``` file to understand the steps and how it is being triggered.

   - Review the trigger defined in the `on:` section to see how this workflow is being run automatically
        
     - The `workflow_dispatch` allows the workflow to be run manually which can be useful when testing.
     - The remaining lines highlight what is going to automatically trigger the workflow. It is being triggered on a push to any branch that is not `main` or `integration`. The changes in the push are also filtered to only include changes made to the 
     `feature_engineering` module. 
   - Review the job starting at the `jobs:` section that has been created already and do the following steps:
     - Check out the repo
     - Logs into Azure
     - Creates an AML job to run the feature engineering module using the [custom action] and the existing [feature engineering job file]

1. Now that the necessary changes have been made, the changes can be pushed to your feature branch which will trigger the feature_engineering_unit_test workflow.

    >**Action Items:**
    >- Run the following commands in sequence to stage changes, commit them, and then push them to your repo:
    1. ```bash 
        git status
        ```

    2. ```bash 
        git add .
        ```

    3. ```bash
        git commit -am "configurations update"
        ```

    4. ```bash
        git push origin yourname-dev
        ```
    >**Note:** After running the above command, credentials of your Github account might be asked for authentication so for **username** just enter your **Github username** and for **password** enter the **PERSONAL ACCESS TOKEN (PAT)** that you generated in **part 0**.
  
    >**Note:** `git status` shows the files that have been modified. It is useful for seeing the latest status of the files, but isn't necessary to commit changes.
   
    >- Check to see if the workflow was properly triggered by going to your GitHub repo and selecting the **Actions tab**.
 
    >**Note:** If the workflow isn't triggered, you can run a workflow under yourname-dev branch under feature_engineering.yml in the Action tab.
   
## The CI CD Workflow is shown below:

![pipeline](images/part3cicd.png)

## Success criteria

- A feature or development branch was created to track your changes.

- Trigger was created on the workflow file ```workshop_unit_test.yml``` to run on a push to your feature branch.
- Understand the additional updates that were made to ```feature_engineering.yml``` file for it to use your secrets and AML resources.
- Workflow was successfully triggered by pushing changes to your feature branch.

## Reference materials
- [GitHub Actions](https://github.com/features/actions)
- [GitHub Actions Workflow Triggers](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)


