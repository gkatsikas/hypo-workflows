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
' OSS Service Order
' =====================

== OSS Service Order Flow ==

SvcPrv -> Web: Authenticate in Portal
Web -> TMF: Create Kubernetes Service Order
TMF -> "TMF\nDB": Store Service Order
TMF -> SONATA: Orchestrate Service Order
SONATA -> OSS_Client: Order Service
OSS_Client -> SONATA: Order Success
SONATA -> TMF: Update Message: Service State ACTIVE 
SONATA -> TMF: Update Message: Service Order State COMPLETED 
```
