```plantuml

' Uncomment this at the end of your design to see only the linked components
hide unlinked

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "Platform\nAdmin" as PltAdmin #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' =====================
' Peering Flow between
' ETSI HypO and ETSI OpenSlice
' =====================

== Peer with remote OpenSlice ==

PltAdmin -> Web: Enters the remote OSL details
Web -> TMF: Crates a TMF632 party organization
TMF -> Web: Returns the created party organization
Web -> Peering: Sends a payload with party organization info 
Peering -> "ETSI\nOpenSlice": Peers and retrieves TMF633 service specifications
Peering -> Web: Returns the service specifications
Web -> Peering: Admin chooses the service specifications to import in HypO catalog 
Peering -> "ETSI\nOpenSlice": API requests the detailed service specifications
"ETSI\nOpenSlice" -> Peering: Specification details are retrieved
Peering -> TMF: Specification details are passed through Kafka
Peering -> Web: Peering success
Web -> PltAdmin: Specifications are now provided through Marketplace

```
