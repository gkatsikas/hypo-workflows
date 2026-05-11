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

== End User Service Update Flow ==
SvcPrv -> Web: Retrieve service
Web -> TMF: Service characteristic update request
TMF -> "TMF\nDB": Service state update PENDING_UPDATE
TMF -> SONATA: Orchestrate service update
SONATA -> Pkg_Manager: Update service deployment
Pkg_Manager -> Compute_Client
Compute_Client -> "Cluster\nController"
"Cluster\nController" -> Compute_Client: Successful service update
Compute_Client -> Pkg_Manager
Pkg_Manager -> SONATA
SONATA -> TMF: Complete service update
TMF -> "TMF\nDB": Store previous state and updated characteristics
TMF -> Web: Service view update
Web -> SvcPrv: Successful service update
```