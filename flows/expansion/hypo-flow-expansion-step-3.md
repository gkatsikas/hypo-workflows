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
' Step 3
' ============================================

note over Web, "Cluster\nController": This flow follows up platform expansion step 2 "OpenZiti client deployment on the new domain"

== Step 3: Register new compute cluster to host an OpenSlice OSS ==

DomainOwner -> Web: Browse on domain compute clusters view
DomainOwner -> Web: Add compute cluster
DomainOwner -> Web: Fill-in domain cluster information\n(i.e., cluster config file)
DomainOwner -> Web: Add cluster
Web -> TMF
TMF -> SONATA: Static compute service onboarding flow
SONATA -> "Fabric\nController": Create secure connection to cluster
"Fabric\nController" -> SONATA: Secure connection created
SONATA -> "Cluster\nController": Authenticate and connect
"Cluster\nController" -> SONATA: Connected
SONATA -> TMF
TMF -> "TMF\nDB": Store compute cluster service into Service Inventory
TMF -> Web: Successful compute\ncluster onboarding
Web -> DomainOwner: Compute cluster visualized

note over Web, "Cluster\nController": Go to step 4 "Order a new OpenSlice OSS for this domain"

```
