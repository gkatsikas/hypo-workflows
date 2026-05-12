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
' User registration
' =====================

== User registration flow ==

User -> PltAdmin: Request an account
PltAdmin -> User: Ask for relevant user information
User -> PltAdmin: Provide the requested info
PltAdmin -> Auth_Manager: Create IAM user and assign user to group
PltAdmin -> TMF: (Optional) Create a TMF organization party\n(if user belongs to an organization)
TMF -> "TMF\nDB": (Optional) Store TMF organization party
PltAdmin -> User: Share credentials with user

```
