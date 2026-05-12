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
' User login
' =====================

== User login Flow ==

SvcPrv -> Web: User arrives in HypO Portal and presses sign in button
Web -> Auth_Manager: Portal redirects to IAM
SvcPrv -> Auth_Manager: Enters credentials
Auth_Manager -> Web: Redirect back to Portal
Web -> SvcPrv: Ask for info in order to create a new tmf party individual
SvcPrv -> Web: User types required information and fills in organization if it exists
Web -> TMF: Creation of tmf party individual to reflect IAM user
Web -> Dashboard_Manager: Creation of a user dashboard 
Web -> SvcPrv: Successful login and redirect to Portal's landing page

```
