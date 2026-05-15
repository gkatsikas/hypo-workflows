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
' Step 5
' ============================================

note over Web, "Cluster\nController": This flow follows up platform expansion step 4 "Order a new OpenSlice OSS for this domain"

== Step 5: OpenSlice OSS resource discovery, service design, and exposure ==



note over Web, "Cluster\nController": Go to workflow "HypO-OpenSlice peering"

```
