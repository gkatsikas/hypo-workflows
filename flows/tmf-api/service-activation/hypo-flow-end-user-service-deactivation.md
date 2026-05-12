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
' End User Service Deactivation
' =====================

== End User Service Deactivation Flow ==

SvcPrv -> Web: Retrieve active service
Web -> TMF: Service deactivation request
TMF -> "TMF\nDB": Service state update PENDING_DEACTIVATION
TMF -> SONATA: Orchestrate service update
SONATA -> Pkg_Manager: Deactivate service
Pkg_Manager -> Compute_Client
Compute_Client -> "Cluster\nController"
"Cluster\nController" -> Compute_Client: Successful service deactivation
Compute_Client -> Pkg_Manager
Pkg_Manager -> SONATA
SONATA -> TMF: Service state INACTIVE
TMF -> "TMF\nDB": Service state update INACTIVE
TMF -> Web: Service view update
Web -> SvcPrv: Successful service update
```
