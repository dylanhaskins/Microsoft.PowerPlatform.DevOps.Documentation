# Config.json

## Location 
```json
<SolutionRoot>/<ProjectName>/Scripts/config.json
```

## Purpose

The `config.json` contains the configuration for a CDS solution which is unpack into source control. This configuration is used by the shared `_Config.ps1` script to configure global variables that are used by downstream scripts such as `_ExportSolution.ps1` and `_GenerateTypes.ps1`

## Definition

| Property     | Type     |                                                   | Description                                                  |
| ------------ | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ServerUrl    | `string`   | Required | The full url of the CDS organization this CDS solution is unpacked from. This includes the protocol (`https`), the organization name (`cdsdev01`) and the region(`crm6`). For example `https://<MyOrgName>.crm6.dynamics.com` |
| SolutionName | `string`   | Required | The logical name of the CDS solution that is unpacked into source control |
| GeoGraphy    | `string` | Required | `//TODO` |
| ProjectName  | `string` | Optional | The name of the `.csproj` that represents the CDS solution. Defaults to SolutionName |
| UnmanagedPackageFile | string | Optional | **Deprecated**                                               |
| ManagedPackageFile | string | Optional | **Deprecated** |

## Examples

### Default configuration

```json
{
    "target": {
        "ServerUrl": "https://<MyOrgName>.crm6.dynamics.com",
        "SolutionName": "<MyCDSSolutionName>",
        "GeoGraphy": "AddGeo"
    }
}
```

### Renamed project

```json
{
    "target": {
        "ServerUrl": "https://<MyOrgName>.crm6.dynamics.com",
        "SolutionName": "<MyCDSSolutionName>",
        "GeoGraphy": "AddGeo",
        "ProjectName": "<csprojName>"
    }
}
```