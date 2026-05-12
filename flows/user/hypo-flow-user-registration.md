```plantuml
hide unlinked
' Uncomment this at the end of your design to see only the linked components

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "User" as User #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' =====================
' User login
' =====================

== User login Flow ==

User -> Web: Sign in
Web -> Auth_Manager: Redirect to IAM
User -> Auth_Manager: Insert credentials
Auth_Manager -> Web: Successful authentication: redirect
Web -> User: Fill in TMF Party form
User -> Web: Insert individual party information and\npotential organization party (if any)
Web -> TMF: Create TMF Party individual/organization
TMF -> "TMF\nDB": Store TMF Party individual/organization
Web -> Dashboard_Manager: Create user account and dashboard
Web -> User: Successful login and redirect to Portal's landing page

```
