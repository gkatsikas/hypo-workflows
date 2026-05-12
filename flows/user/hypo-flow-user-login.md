```plantuml

hide unlinked
' Uncomment this at the end of your design to see only the linked components

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "User" as User #000000
actor "Platform\nAdmin" as PltAdmin #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' =====================
' User creation and login
' =====================

== User creation flow ==

User -> PltAdmin: Request an account
PltAdmin -> User: Ask for information about partner organization
User -> PltAdmin: Provide the requested info
PltAdmin -> Auth_Manager: Create IAM user and assign user to group
PltAdmin -> TMF: (Optional) Create a TMF organization party\n(if user belongs to an organization)
TMF -> "TMF\nDB": (Optional) Store TMF organization party
PltAdmin -> User: Share credentials with user

== User login flow ==

User -> Web: Login with credentials
Web -> Auth_Manager: Authenticate
Auth_Manager -> Web: Successful authentication
Web -> User: Welcome to HypO's landing page

```
