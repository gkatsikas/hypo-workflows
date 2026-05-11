```plantuml

' Uncomment this at the end of your design to see only the linked components
hide unlinked

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

== Kubernetes Service Termination Flow ==
SvcPrv -> Web: Retrieve K8s service
Web -> TMF: K8s service termination request
TMF -> "TMF\nDB": Service state update PENDING_TERMINATION
TMF -> SONATA: Orchestrate K8s service termination
SONATA -> OSS_Client: Terminate K8s service
OSS_Client -> "ETSI\nOpenSlice"
"ETSI\nOpenSlice" -> "Cluster\nNode": Tear down
"ETSI\nOpenSlice" -> "Cluster\nController": Tear down
"ETSI\nOpenSlice" -> OSS_Client: Successful K8s service termination
OSS_Client -> SONATA
SONATA -> Fabric: Terminate private connection to Kubernetes
Fabric -> "Fabric\nController": Termination of encrypted connection
"Fabric\nController" -> Fabric: Encrypted connection terminated
Fabric -> SONATA: Successful connection termination
SONATA -> TMF: Service state TERMINATED
TMF -> "TMF\nDB": Store service state TERMINATED
TMF -> Web: Service view update
Web -> SvcPrv: Successful K8s service termination
```
