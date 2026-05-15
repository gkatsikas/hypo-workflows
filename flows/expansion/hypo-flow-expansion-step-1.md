```plantuml

' Uncomment this at the end of your design to see only the linked components
hide unlinked

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "Domain\nOwner" as DomainOwner #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' ============================================
' Platform expansion to new private domain
' Step 1
' ============================================

note over Web, "Fabric\nController": This flow follows up platform expansion step 0 "Registration of the domain owner"

== Step 1: Platform expansion request ==

DomainOwner -> Web: Login
Web -> Auth_Manager: Authenticate
Auth_Manager -> Web: Authenticated
Web -> DomainOwner: Successful login
DomainOwner -> Web: Browse on platform expansion view
Web -> Fabric: Create an identity for the new domain
Fabric -> "Fabric\nController": Authenticate with HypO credentials
"Fabric\nController" -> Fabric: Successful authentication
Fabric -> "Fabric\nController": Create domain identity
"Fabric\nController" -> Fabric: Domain identity created
Fabric -> Web
Web -> DomainOwner: Domain identity checkout button
DomainOwner -> Web: Download domain identity locally

note over Web, "Fabric\nController": Go to step 2 "OpenZiti client deployment on the new domain"

```
