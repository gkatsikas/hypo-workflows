```plantuml
hide unlinked
' Uncomment this at the end of your design to see only the linked components

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "Service\nProvider" as SvcPrv #000000
actor "Platform\nAdmin" as PltAdmin #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' =====================
' User registration
' =====================

== User registration Flow ==

SvcPrv -> PltAdmin: Ask for HypO account
PltAdmin -> SvcPrv: Ask for information about partner organization
SvcPrv -> PltAdmin: Provides the requested info
PltAdmin -> Auth_Manager: Create Keycloak user and adds user to group
PltAdmin -> TMF: (Optional) Creates a tmf party organization if partner belongs to an org
PltAdmin -> SvcPrv: Contacts partner with created HypO user credentials
```
