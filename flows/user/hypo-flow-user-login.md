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

== User login flow ==

User -> Web: Sign in
Web -> Auth_Manager: Redirect to IAM
User -> Auth_Manager: Insert credentials
Auth_Manager -> Web: Successful authentication: redirect
Web -> User: Fill in TMF party form
User -> Web: Insert individual party information and\npotential organization party (if any)
note over User, TMF: If an organization party was created during registration,\nit is linked with the individual party created here
Web -> TMF: Create TMF party individual\n(optionally with related organization party)
TMF -> "TMF\nDB": Store TMF party individual
Web -> Dashboard_Manager: Create user account
Web -> User: Successful login and redirect to Portal's landing page

```
