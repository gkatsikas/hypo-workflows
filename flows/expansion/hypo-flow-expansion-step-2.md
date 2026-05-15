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
' Step 2
' ============================================

note over Web, "Cluster\nController": This flow follows up platform expansion step 1 "Platform expansion request"

== Step 2: OpenZiti client deployment on the new domain ==

DomainOwner -> "Cluster\nController": Deploy OpenZiti Client with domain identity
"Cluster\nController" -> "Fabric Client\nRemote": Deploy
"Fabric Client\nRemote" -> "Fabric\nController": Authenticate with domain identity
"Fabric\nController" -> "Fabric Client\nRemote": Successful authentication
Fabric -> "Fabric\nController": Periodic pull of domain identities
"Fabric\nController" -> Fabric: Identities fetched
Fabric -> Web: Domain identities update view
Web -> DomainOwner: New domain is connected

note over Web, "Cluster\nController": Go to step 3 "Register new compute cluster to host an OpenSlice OSS"

```
