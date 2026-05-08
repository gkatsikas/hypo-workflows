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

SvcPrv -> Web: Authenticate in Portal
Web -> TMF: Create End User Service Order: provide Registry Info and Kubernetes Service ID 
TMF -> SONATA: Orchestrate Service Order
SONATA -> Pkg_Manager: Parse Helm Engine Chart: Provide Registry Info
Pkg_Manager -> SONATA: Parse Successful
SONATA -> Pkg_Manager: Deploy Helm Engine Chart: Provide Kubernetes Service Id for deployment
Pkg_Manager -> SONATA: Deployment Successful
SONATA -> Telemetry_Client: Create Grafana and Loki Dashboards for service
Telemetry_Client -> SONATA: Report Success
SONATA -> TMF: Update Message: Service State ACTIVE 
SONATA -> TMF: Update Message: Service Order State COMPLETED 
```