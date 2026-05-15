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
' Step 4
' ============================================

note over Web, "Cluster\nController": This flow follows up platform expansion step 3 "Register new compute cluster to host an OpenSlice OSS"

== Step 4: Order a new OpenSlice OSS for this domain ==

DomainOwner -> Web: Browse on service Marketplace
DomainOwner -> Web: Add relevant service specification into shopping cart
Web -> Cart
DomainOwner -> Web: Configure service registry info, Kubernetes service ID
DomainOwner -> Web: Place service order
Web -> TMF: Dispatch service order
TMF -> SONATA: Service order management flow
SONATA -> "Cluster\nController": Authenticate and connect
SONATA -> "Cluster\nController": Deploy OpenSlice service package
"Cluster\nController" -> "ETSI\nOpenSlice": Deploy
"Cluster\nController" -> SONATA: Deployed
SONATA -> TMF: Successful OpenSlice service provisioning
TMF -> "TMF\nDB": Store OpenSlice service into Service Inventory
TMF -> Web: Service order Completed
Web -> DomainOwner: OpenSlice service available on My Services

note over Web, "Cluster\nController": Go to step 5 "OpenSlice OSS resource discovery, service design, and exposure"

```
