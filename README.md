[toc]

# Documentation and user guide

[For a detailed instruction on the toolset, link via 365.training](https://365.training/Instructors/detail/EugenevanStaden)

## Pre-requisites:

- PowerShell minimum version [TBC]
- Administrative access on your installation device
- Azure DevOps
    - Access to Azure DevOps Project with account [access level Basic or Visual Studio Subscription (not stakeholder)](https://docs.microsoft.com/en-us/azure/devops/organizations/security/access-levels?view=azure-devops#supported-access-levels)
- CDS 

## Terminology
| Term | Description |
|--|--|
| ADO | Azure DevOps |
| CDS | Common Data Service |

## Setup

| Action | PowerShell Cmdlet | Steps |
|--|--|--|
| **Installing the module** | `Install-Module -Name Microsoft.PowerPlatform.DevOps` | 1. Run 'Windows PowerShell' as an administrator<br>2. Run the cmdlet <br>_Note: Other installation methods can be found at https://www.powershellgallery.com/packages/Microsoft.PowerPlatform.DevOps_ |
| **Using the module** | `Invoke-PowerPlatformDevOps` | 1. Run the cmdlet <br>_Note: It is recommended that you open PowerShell as administrator_ |
| **Find what version you have installed**  | `Get-InstalledModule Microsoft.PowerPlatform.DevOps` | 1. Run the cmdlet <br>_Note: Your current running version is also specified on the top of the screen when you invoke the module_ |  |
| **Find newer version** | `[U]` | 1. `Invoke-PowerPlatformDevOps` <br>2. Select `[U]` to check if there are newer versions available |  |
| **Update your version** | `Update-Module Microsoft.PowerPlatform.DevOps -Force` | 1. Run the cmdlet |  |

# Using the tool

| # | Step | Description |
|--|--|--|
| 1 | Run Pre-requisite checks (Install / Update) | This step installs the relevant dependencies required by the tool  (e.g. git, node.js, etc. )|
| 2 | Create a New Project or Select Existing | To set up and connect the project for use in the tool |
| 3 | Configure Azure DevOps _(ADO Org: sampleOrg \| ADO Project: SampleADOProject \| git Repo: sampleRepo )_ | Create or connect to an ADO Project |
| 4 | Add New D365 / CDS Solution | Add a solution from a CDS environment to your local repository |
| 5 | Configure Continuous Deployment _(CI/CD Environment : Staging01 \| CI/CD URL : https://example.crm6.dynamics.com)_ | Add staging environment |
| A | Enable [A]zure Resource Management Deployment |  |
| F | Add Azure [F]unction App Project |
| D | Add Additional [D]365 / CDS Solutions |
| E | [E]xport & Unpack Solution to Source Control |
| S | Commit and [S]ync changes to Source Control |
| V | [V]iew current change log for Source Control |
| T | Add Additional Deployment Environment [T]arget |
| U | Check for [U]pdates to Microsoft.PowerPlatform.DevOps |
| Q | Press 'Q' to quit |

## 2 - Create a New Project or Select Existing

| Option | Description |
|--|--|
| Select an existing project | Connect to a local project repository you have previously connected to using the tool 
| Browse for local repository | Connect to a local project repository by browsing your file directory |
| Create a new project | Create and connect a new local project repository |
| Clone an existing repo | Clone an existing repository from ADO |

## 3 - Configure Azure DevOps

- Connects to your ADO organisation and project
- Connects your local repository to ADO

**Outcomes:**

- Local repository is set up to be connected to ADO, configurations are retained in _&lt;YourADORepo&gt;.json_ file

    ```json
    {
        "ID":  "",
        "Name":  "",
        "ProjectLocation":  "",
        "ADOProject":  "SampleADOProject",
        "gitRepo":  "SampleRepo",
        "ADOOrgName":  "SampleOrg",
        "ADOConfigured":  "True",
        "SolutionAdded":  "False",
        "CICDEnvironmentName":  "False",
        "CICDEnvironmentURL":  "",
        "CICDVarGroupID":  "",
        "CIPipeLineId":  "",
        "ARMAdded":  "Optional",
        "FunctionAppAdded":  "Optional",
        "ServicePrincipal":  "Optional",
        "CDSSolutions": [

                        ],
        "selectedSubscription":  "00000000-0000-0000-0000-000000000000",
        "selectedSubscriptionName":  "Sample Subscription",
        "AzureKeyVaultName":  "",
        "ClientID":  "",
        "ClientSecretAKVName":  "",
        "TenantID":  "",
        "EnvironmentSecurityID":  ""
    }
    ```

## 4 - Add New D365 / CDS Solution

- Add a solution from a CDS environment to your local repository

**Outcomes:**

- Commit in git history for adding solution and related solution files
    - Including an update in _deployPackages.json_ with reference to your new solution

        ```json
        [
            { 
                "DestinationFolder": "SolutionOne",
                "PackageFolder": "SolutionOne",
                "PackageName": "SolutionOnePackage.dll",
                "SolutionName": "SolutionOne",
                "DeployTo": [
                    {
                        "EnvironmentName": "Deployment Staging",
                        "DeploymentType": "Managed",
                        "DeployData": "true",
                        "PreAction": "false",
                        "PostAction": "false"
                    }
                ],
                "DeploymentSteps": "",
            }
        ]
        ```

- _&lt;YourADORepo&gt;.json_ file updated with solution reference

    ```json
    {
        "ID":  "",
        "Name":  "",
        "ProjectLocation":  "",
        "ADOProject":  "SampleADOProject",
        "gitRepo":  "SampleRepo",
        "ADOOrgName":  "SampleOrg",
        "ADOConfigured":  "True",
        "SolutionAdded":  "True",
        "CICDEnvironmentName":  "False",
        "CICDEnvironmentURL":  "",
        "CICDVarGroupID":  "",
        "CIPipeLineId":  "",
        "ARMAdded":  "Optional",
        "FunctionAppAdded":  "Optional",
        "ServicePrincipal":  "Optional",
        "CDSSolutions": [
                            {
                                "SolutionName":  "SolutionOne",
                                "ID":  0
                            }
                        ],
        "selectedSubscription":  "00000000-0000-0000-0000-000000000000",
        "selectedSubscriptionName":  "Sample Subscription",
        "AzureKeyVaultName":  "",
        "ClientID":  "",
        "ClientSecretAKVName":  "",
        "TenantID":  "",
        "EnvironmentSecurityID":  ""
    }
    ```

## 5 - Configure Continuous Deployment

- Connects to your CDS staging environment
- Adds pipeline [environment](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/environments)
- Adds credentials as [variables](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups) in pipeline [library](https://docs.microsoft.com/en-us/azure/devops/pipelines/library)

**Outcomes:**

- _&lt;YourADORepo&gt;.json_ file updated with staging environment details

    ```json
        {
            "ID":  "",
            "Name":  "",
            "ProjectLocation":  "",
            "ADOProject":  "SampleADOProject",
            "gitRepo":  "SampleRepo",
            "ADOOrgName":  "SampleOrg",
            "ADOConfigured":  "True",
            "SolutionAdded":  "True",
            "CICDEnvironmentName":  "Staging",
            "CICDEnvironmentURL":  "https://staging.crm6.dynamics.com",
            "CICDVarGroupID":  "1",
            "CIPipeLineId":  "1",
            "ARMAdded":  "Optional",
            "FunctionAppAdded":  "Optional",
            "ServicePrincipal":  "Optional",
            "CDSSolutions": [
                                {
                                    "SolutionName":  "SolutionOne",
                                    "ID":  0
                                }
                            ],
            "selectedSubscription":  "00000000-0000-0000-0000-000000000000",
            "selectedSubscriptionName":  "Sample Subscription",
            "AzureKeyVaultName":  "",
            "ClientID":  "",
            "ClientSecretAKVName":  "",
            "TenantID":  "",
            "EnvironmentSecurityID":  ""
        }
    ```

- New 'Staging' environment in ADO
- New variable group in ADO

## T - Add Additional Deployment Environment [T]arget

- Connects additional target environment
- Adds pipeline [environment](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/environments)
- Adds credentials as [variables](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/variable-groups) in pipeline [library](https://docs.microsoft.com/en-us/azure/devops/pipelines/library)
- _Note:_ Further configuration is required in _deployPackages.json_ to define environments to deploy a solution to

**Outcomes:**

- _build.yaml_ file appended with new environment

    ```yaml
    - stage: Test
        
        displayName: Test
        dependsOn: 'Deployment_Staging'
        condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/master'),notIn(variables['Build.Reason'], 'IndividualCI', 'PullRequest'))
        jobs:
        - deployment: DeployJob      
        displayName: Test 
        environment: 'Test'
        variables:
        - group: SampleRepo.D365TestEnvironment
        strategy:
        runOnce:
            deploy:
            steps:
            - task: PowerShell@2
                displayName: 'Deploy Solution'
                inputs:
                targetType: filePath
                filePath: '$(Pipeline.Workspace)/drop/Solutions/Scripts/SolutionDeploy.ps1'
                arguments: '-DeployServerUrl $(d365url) -UserName $(d365username) -Password $(d365password) -PipelinePath $(Pipeline.Workspace)'
    ```
- New 'Test' environment in ADO
- New variable group in ADO

# Things to know
| Category | Q | A |
|--|--|--|
| Setup | Run Pre-requisite checks (Install / Update) is erroring out | [Check/set your PowerShell execution policy to bypass](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy) |
|  | Where do I set solution ordering/layering  | This is configured in: _&lt;YourADORepo&gt;.json_ |
|  | How do I set individual build to go to specific environments | This is configured in: _build.yaml_<br>This is configured by:  |
| Build | When should I build in Debug mode? |  |
| Build | When should I build in Release mode? |  |
| Build | When should I build in SolutionPackager mode? |  |
| Build | When should I build in GenerateXRMTypes mode? |  |
|  | How do I find the source environment for a solution? | This is configured in: ..._&lt;solutionName&gt;/scripts/config.json_ |
