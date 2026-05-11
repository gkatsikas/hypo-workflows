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
' 5G Service Termination
' =====================

== 5G Service Termination Flow ==
SvcPrv -> Web: Retrieve 5G Service
Web -> TMF: Service termination request
TMF -> "TMF\nDB": Service state update PENDING_TERMINATION
TMF -> SONATA: Orchestrate 5G service termination
SONATA -> OSS_Client: Terminate 5G service
OSS_Client -> "ETSI\nOpenSlice"
"ETSI\nOpenSlice" -> "5G\nSystem"
"5G\nSystem" -> "ETSI\nOpenSlice": Successful 5G service termination
"ETSI\nOpenSlice" -> OSS_Client
OSS_Client -> SONATA
SONATA -> TMF: Service state TERMINATED
TMF -> "TMF\nDB": Store service state TERMINATED
TMF -> Web: Service view update
Web -> SvcPrv: Successful 5G service termination
```