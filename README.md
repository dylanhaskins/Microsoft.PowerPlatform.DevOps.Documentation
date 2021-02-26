# Documentation and user guide

[For a detailed instruction on the toolset, link via 365.training](https://365.training/Player/VideoPlayer/8e5e028b-bb03-4c27-bba3-8e3edda5c76e/b4b58a35-9209-eb11-a813-000d3a58ba85)

### Prerequisites:

* PowerShell minimum version [TBC]
* Administrative access on your installation device

## Setup

| Action | PowerShell Cmdlet | Steps |
|--|--|--|
| **Installing the module** | `Install-Module -Name Microsoft.PowerPlatform.DevOps` | 1. Run 'Windows PowerShell' as an administrator<br>2. Run the cmdlet <br>_Note: Other installation methods can be found at https://www.powershellgallery.com/packages/Microsoft.PowerPlatform.DevOps_ |
| **Using the module** | `Invoke-PowerPlatformDevOps` | 1. Run the cmdlet <br>_Note: It is recommended that you open PowerShell as administrator_ |
| **Find what version you have installed**  | `Get-InstalledModule Microsoft.PowerPlatform.DevOps` | 1. Run the cmdlet <br>_Note: Your current running version is also specified on the top of the screen when you invoke the module_ |  |
| **Update your version** | `Update-Module Microsoft.PowerPlatform.DevOps` | 1. Run the cmdlet |  |
| **Update your version** | `[U]` | 1. `Invoke-PowerPlatformDevOps` <br>2. Select `[U]` to Update your tool |  |

## Using the tool

| # | Step | Description |
|--|--|--|
| 1 | Run Pre-requisite checks (Install / Update) | This step installs the relevant dependencies required by the tool  (e.g. git, node.js, etc. )|
| 2 | Create a New Project or Select and Existing One | To set up and connect the project for use in the tool |
| 3 | Configure Azure DevOps (ADO Org:  \| ADO Project:  \| git Repo: <<your repo name>> ) | Create/connect to the Azure DevOps Project |
| 4 | Add New D365 / CDS Solution |  |
| 5 | Configure Continuous Deployment (CI/CD Environment : Staging01 \| CI/CD URL : https://example.crm6.dynamics.com) |  |
| A | Enable [A]zure Resource Management Deployment |  |
| F | Add Azure [F]unction App Project |
| D | Add Additional [D]365 / CDS Solutions |
| E | [E]xport & Unpack Solution to Source Control |
| S | Commit and [S]ync changes to Source Control |
| V | [V]iew current change log for Source Control |
| T | Add Additional Deployment Environment [T]arget |
| U | Check for [U]pdates to Microsoft.PowerPlatform.DevOps |
| Q | Press 'Q' to quit |


### 2 Create a New Project or Select an Existing One

| Option | Description |
|--|--|
| Select an existing project | Connect to an existing local project repository you have previously connected to in the past |
| Browse for local repository | Connect to an existing local project repository by browsing your file directory |
| Create a new project | Create and connect a new local project repository |
| Clone an existing repo | Clone an existing repository from Azure DevOps |

### 3 Configure Azure DevOps

| Step | Description | Input |
|--|--|--|
| 1 | Enter your Azure DevOps organisation (e.g. dev.azure.com/**testingOrg**) | testingOrg |
| 2 | Select  |  |
|  |  |  |
|  |  |  |
|  |  |  |

Once connected (ADO Org: testingOrg | ADO Project: sampleProject | git Repo: myProject )