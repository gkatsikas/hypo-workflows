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
' End User Service Termination
' =====================

== End User Service Terminate Flow ==
SvcPrv -> Web: Authenticate in Portal
SvcPrv -> Web: Retrieve Service
Web -> TMF: Submit a Service Termination 
TMF -> "TMF_DB": Service state update PENDING_TERMINATION
TMF -> SONATA: Orchestrate Service Termination
SONATA -> Pkg_Manager: Delete service package deployment
Pkg_Manager -> SONATA: Successful deployment deletion
SONATA -> Telemetry_Client: Delete service telemetry and log dashboards
Telemetry_Client -> SONATA: Successful deletion of dashboards
SONATA -> TMF: Service state TERMINATED
TMF -> "TMF\nDB": Store Service state TERMINATED
TMF -> Web: Service view update
Web -> SvcPrv: Successful service termination
```