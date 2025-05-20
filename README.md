# xc-ad-user-audit

This PowerShell script queries an F5 Distributed Cloud (XC) tenant for a list of user roles and verifies whether the associated email accounts exist in Microsoft Entra ID (formerly Azure AD) using Microsoft Graph.

## Prerequisites

- PowerShell 7+ (Windows, macOS, or Linux)
- [Microsoft.Graph](https://www.powershellgallery.com/packages/Microsoft.Graph) PowerShell module:

  ```powershell
  Install-Module Microsoft.Graph -Scope CurrentUser
  ```

- Valid credentials to authenticate with Microsoft Graph (User.Read.All scope)

- An F5 XC API token with access to the user_roles API

## Script Parameters

- TenantDomain: Your F5 XC tenant domain (e.g. tenant.console.ves.volterra.io)
- ApiToken: F5 XC API token (APIToken <token>)
- OutputFormat: Table, CSV, or Text (default: Table)

## Usage

```powershell
# Basic usage with table output
.\Verify-XCUserAccounts.ps1 `
  -TenantDomain "tenant.console.ves.volterra.io" `
  -ApiToken "your_api_token_here"

# Output results to CSV
.\Verify-XCUserAccounts.ps1 `
  -TenantDomain "tenant.console.ves.volterra.io" `
  -ApiToken "your_api_token_here" `
  -OutputFormat "CSV"

# Output as simple text
.\Verify-XCUserAccounts.ps1 `
  -TenantDomain "tenant.console.ves.volterra.io" `
  -ApiToken "your_api_token_here" `
  -OutputFormat "Text"
```

### Output Examples

## Table (default)

```pgsql
Email                         ExistsInAzureAD
-----                         ----------------
admin@example.com             Yes
user.notfound@example.com     No
```

## CSV

Exports to XCUserCheck_YYYYMMDD_HHMMSS.csv in the current directory.

## Text

```scss
admin@example.com: Yes
user.notfound@example.com: No
```

### Security Notes

- The API token is passed via header using the APIToken scheme.

- No token information is written to disk.

- Ensure that your API token is kept secure and scoped appropriately.
