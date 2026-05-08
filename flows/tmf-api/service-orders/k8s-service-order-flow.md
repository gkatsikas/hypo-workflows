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

SvcPrv -> Web: Authenticate in Portal
Web -> TMF: Create Kubernetes Service Order
TMF -> "TMF\nDB": Store Service Order
TMF -> SONATA: Orchestrate Service Order
SONATA -> OSS_Client: Order Kubernetes
OSS_Client -> "ETSI\nOpenSlice"
OSS_Client -> SONATA: Order Success: return kubeConf file
SONATA -> Registry: Store kubeConf
Registry -> "Secrets\nDB": Store kubeConf with key Kubernetes TMF Service ID
Registry -> SONATA: Successful Storage of kubeConf
SONATA -> Fabric: Domain Connection Request for Kubernetes IP and Port
Fabric -> "Fabric\nController": Create Domain Connection
"Fabric\nController" -> Fabric: Domain Connection created
Fabric -> SONATA: Domain Connection Creation Success
SONATA -> TMF: Update Message: Service State ACTIVE 
SONATA -> TMF: Update Message: Service Order State COMPLETED 

```
