```plantuml
hide unlinked
' Uncomment this at the end of your design to see only the linked components

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "Service\nProvider" as SvcPrv #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' =====================
' Kubernetes Service Order
' =====================

== Kubernetes Service Order Flow ==

SvcPrv -> Web: Authenticate
SvcPrv -> Web: Browse service marketplace
SvcPrv -> Web: Find "K8saaS" service specification
SvcPrv -> Web: Add "K8saaS" service specification into shopping cart
SvcPrv -> Web: Configure number and flavor of K8s nodes
SvcPrv -> Web: Place service order
Web -> TMF: Dispatch service order
TMF -> "TMF\nDB": Store service order
TMF -> SONATA: Orchestrate service order
SONATA -> OSS_Client: Order "K8saaS" from OpenSlice
OSS_Client -> "ETSI\nOpenSlice"
"ETSI\nOpenSlice" -> "Cluster\nController": Create
"ETSI\nOpenSlice" -> "Cluster\nNode": Create (repeated if workers > 1)
"ETSI\nOpenSlice" -> OSS_Client: Service order state COMPLETED
OSS_Client -> SONATA: Successful service order:\nkubeConf file is available
SONATA -> Registry: Store kubeConf
Registry -> "Secrets\nDB"
Registry -> SONATA: Successful storage of kubeConf
SONATA -> Fabric: Establish private connection to Kubernetes
Fabric -> "Fabric\nController": Create encrypted connection
"Fabric\nController" -> Fabric: Encrypted connection created
Fabric -> SONATA: Successful connection
SONATA -> TMF: Service state ACTIVE
SONATA -> TMF: Service order state COMPLETED
TMF -> Web: Service order view update
Web -> SvcPrv: Successful service order
```
