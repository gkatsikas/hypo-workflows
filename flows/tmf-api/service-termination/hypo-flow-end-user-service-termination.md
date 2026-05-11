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

== End User Service Termination Flow ==
SvcPrv -> Web: Retrieve end user service
Web -> TMF: Service termination request
TMF -> "TMF\nDB": Service state update PENDING_TERMINATION
TMF -> SONATA: Orchestrate end user service termination
SONATA -> Pkg_Manager: Deprovision service package
Pkg_Manager -> Compute_Client
Compute_Client -> "Cluster\nController"
"Cluster\nController" -> Compute_Client: Service package deprovisioned
Compute_Client -> Pkg_Manager
Pkg_Manager -> SONATA
SONATA -> Telemetry_Client: Delete service telemetry and log dashboards
Telemetry_Client -> SONATA: Successful deletion of dashboards
SONATA -> TMF: Service state TERMINATED
TMF -> "TMF\nDB": Store service state TERMINATED
TMF -> Web: Service view update
Web -> SvcPrv: Successful end user service termination
```