# deployPackages.json

## Location 
```json
<SolutionRoot>/deployPackages.json
```

## Purpose

The `deployPackages.json` determines which CDS solutions will deployed, and which environments they will deploy to. The root element is an array which contains one or more objects which defines the deployment strategy for a single CDS solution.

## Definition

| Property     | Type     |                                                   | Description                                                  |
| ------------ | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| DestinationFolder | `string`   | Required | The name of the folder where the unpacked solution will be copied to inside the `bin/Release/PackageDeployer/` folder |
| PackageFolder | `string`   | Required | The name of the folder where the unpacked solution will be copied to inside the `bin/Release/PackageDeployer/` folder |
| PackageName | `string` | Required | The name of the assembly that defines the solution import actions. This assembly is built from the file at `<SolutionRoot>/<Project>/Deployment/<ProjectName>Package.cs`. e.g. `MyProjectPackage.dll` |
| SolutionName | `string` | Required | The logical name of the CDS solution                         |
| DeploymentSteps | `string` | Optional |                                                              |
| DeployTo | `Array` | Optional | An array of one or more environments to deploy this CDS solution to, along with configuration for pre-actions, post-actions, deployment type and deploy data |

### DeployTo
| Property     | Type     | Required | Allowed Values                                | Description                                                  |
| ------------ | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| EnvironmentName | `string`   | Required |  | The name of the environment as defined in the `build.yaml` |
| DeploymentType | `string`   | Required | `managed` `unmanaged` | Define how the solution is deployed to the target environment. Expects `managed`, `unmanaged` |
| DeployData | `boolean` | Required | `true` `false`        | Enable or disable the deployment of data bundled into the packaged solution |
| PostAction | `boolean` | Required | `true` `false` | Enable the pre actions to run when this solution is deployed to a particular environment. The pre actions are defined in `<SolutionRoot>/<Project>/Scripts/PreAction.ps1` |
| PreAction | `boolean` | Required | `true` `false` | Enable the post actions to run when this solution is deployed to a particular environment. The post actions are defined in `<SolutionRoot>/<Project>/Scripts/PostAction.ps1` |

## Examples

### Default configuration

```json
[
    {
        "DeploymentSteps": "",
        "SolutionName": "ClientCore",
        "PackageFolder": "ClientCore",
        "DeployTo": [
            {
                "EnvironmentName": "Deployment Staging",
                "DeploymentType": "Managed",
                "DeployData": "true",
                "PreAction": "false",
                "PostAction": "false"
            },
            {
                "EnvironmentName": "Deployment Test",
                "DeploymentType": "Managed",
                "DeployData": "true",
                "PreAction": "false",
                "PostAction": "false"
            }
        ],
        "DestinationFolder": "ClientCore",
        "PackageName": "ClientCorePackage.dll"
    },
    {
        "DeploymentSteps": "",
        "PackageFolder": "ClientApps",
        "SolutionName": "ClientApps",
        "DeployTo": [
            {
                "EnvironmentName": "Deployment Staging",
                "DeploymentType": "Managed",
                "DeployData": "false",
                "PreAction": "false",
                "PostAction": "false"
            },
            {
                "EnvironmentName": "Deployment Test",
                "DeploymentType": "Managed",
                "DeployData": "false",
                "PreAction": "false",
                "PostAction": "false"
            }
        ],
        "DestinationFolder": "ClientApps",
        "PackageName": "ClientAppsPackage.dll"
    }
]
```