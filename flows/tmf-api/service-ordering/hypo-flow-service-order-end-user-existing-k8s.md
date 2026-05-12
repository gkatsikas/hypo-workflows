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
' End User Service Order
' =====================

== End User Service Order Flow ==

SvcPrv -> Web: Browse service marketplace
SvcPrv -> Web: Add service specification into shopping cart
SvcPrv -> Web: Configure service registry info and Kubernetes service ID
SvcPrv -> Web: Place service order
Web -> TMF: Dispatch service order
TMF -> "TMF\nDB": Store service order
TMF -> SONATA: Orchestrate service order
SONATA -> Pkg_Manager: Parse service package
Pkg_Manager -> SONATA: Successful parsing
SONATA -> Pkg_Manager: Deploy service package
Pkg_Manager -> Compute_Client
Compute_Client -> "Cluster\nController": Deploy
"Cluster\nController" -> Compute_Client: Successful deployment
Compute_Client -> Pkg_Manager:
Pkg_Manager -> SONATA: Successful service package deployment
SONATA -> Telemetry_Client: Create service telemetry and log dashboards

note over Dashboard_Manager, "Cluster\nController": Service telemetry setup
Telemetry_Client -> Telemetry_Manager: Register service metrics
Telemetry_Manager -> "Cluster\nController": Pull metrics
Telemetry_Client -> Dashboard_Manager: Design metrics' dashboard
Dashboard_Manager -> Telemetry_Manager: Pull metrics' values
Telemetry_Client -> SONATA: Telemetry dashboard created

note over Dashboard_Manager, "Cluster\nController": Service logs setup
Telemetry_Client -> Log_Manager: Request service logs
Log_Manager -> "Cluster\nController": Subscribe to logs
"Cluster\nController" -> Log_Manager: Logs reporting
Log_Manager -> Dashboard_Manager: Populate service logs on dashboard
Log_Manager -> Telemetry_Client: Successful logs reporting
Telemetry_Client -> SONATA: Log dashboard created

SONATA -> TMF: Service state ACTIVE
SONATA -> TMF: Service order state COMPLETED
TMF -> Web: Service order view update
Web -> SvcPrv: Successful service order
```