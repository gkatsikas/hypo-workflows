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

SvcPrv -> Web: Authenticate
SvcPrv -> Web: Retrieve Inactive Service
Web -> TMF: Submit a Service Activation 
TMF -> "TMF\nDB": Service state update PENDING_ACTIVATION
TMF -> SONATA: Orchestrate Service Update
SONATA -> Pkg_Manager: Request to Activate Service
Pkg_Manager -> SONATA: Successful Service Activation
SONATA -> TMF: Service state ACTIVE
TMF -> "TMF\nDB": Store Service state ACTIVE
TMF -> Web: Service view update
Web -> SvcPrv: Successful service update
```
