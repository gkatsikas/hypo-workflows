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
' End User Service Activation
' =====================

== End User Service Activation ==

SvcPrv -> Web: Retrieve inactive service
Web -> TMF: Service activation request
TMF -> "TMF\nDB": Service state update PENDING_ACTIVATION
TMF -> SONATA: Orchestrate service update
SONATA -> Pkg_Manager: Activate service
Pkg_Manager -> Compute_Client
Compute_Client -> "Cluster\nController"
"Cluster\nController" -> Compute_Client: Successful service activation
Compute_Client -> Pkg_Manager
Pkg_Manager -> SONATA
SONATA -> TMF: Service state ACTIVE
TMF -> "TMF\nDB": Service state update ACTIVE
TMF -> Web: Service view update
Web -> SvcPrv: Successful service update
```
