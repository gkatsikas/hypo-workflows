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

SvcPrv -> Web: Authenticate
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
Pkg_Manager -> SONATA: Successful deployment
SONATA -> Telemetry_Client: Create service telemetry and log dashboards
Telemetry_Client -> SONATA: Successful reporting of dashboards
SONATA -> TMF: Service state ACTIVE
SONATA -> TMF: Service order state COMPLETED
TMF -> Web: Service order view update
Web -> SvcPrv: Successful service order
```