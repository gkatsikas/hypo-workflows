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
' Kubernetes Service Termination
' =====================

== Kubernetes Service Termination Flow ==
SvcPrv -> Web: Authenticate
SvcPrv -> Web: Retrieve 5G Service
Web -> TMF: Submit a Service Termination 
TMF -> "TMF\nDB": Service state update PENDING_TERMINATION
TMF -> SONATA: Orchestrate 5G Service Termination
SONATA -> OSS_Client: Terminate 5G Service
OSS_Client -> "ETSI\nOpenSlice"
"ETSI\nOpenSlice" -> OSS_Client: Successful Service Termination
OSS_Client -> SONATA: Report Success
SONATA -> TMF: Service state TERMINATED
TMF -> "TMF\nDB": Store Service state TERMINATED
TMF -> Web: Service view update
Web -> SvcPrv: Successful 5G service termination
```