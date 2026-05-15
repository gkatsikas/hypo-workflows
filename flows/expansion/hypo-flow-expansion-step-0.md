```plantuml

' Uncomment this at the end of your design to see only the linked components
hide unlinked

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "Domain\nOwner" as DomainOwner #000000
actor "Platform\nAdmin" as PltAdmin #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' ============================================
' Platform expansion to new private domain
' Step 0
' ============================================

note over Web, Auth_Manager: This flow initiates platform expansion to a new private domain.\nIt assumes ETSI HypO has already peered with OpenZiti.

== Step 0: Registration of the domain owner ==

DomainOwner -> PltAdmin: Request an ETSI HypO account
PltAdmin -> DomainOwner: Ask for relevant user information
DomainOwner -> PltAdmin: Provide the requested info
PltAdmin -> Web: Input user information
Web -> Auth_Manager: Create user and assign user to group
Web -> TMF: Create a TMF organization party\n(if user belongs to an organization)
TMF -> "TMF\nDB": Store user
TMF -> Web: New user (with potentially associated TMF party) is created
Web -> PltAdmin
PltAdmin -> DomainOwner: Share credentials with new domain owner

note over Web, Auth_Manager: Go to step 1 "Platform expansion request"

```
