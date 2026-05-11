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

SvcPrv -> Web: Authenticate
SvcPrv -> Web: Retrieve Active Service
Web -> TMF: Submit a Service Deactivation 
TMF -> "TMF\nDB": Service state update PENDING_DEACTIVATION
TMF -> SONATA: Orchestrate Service Update
SONATA -> Pkg_Manager: Request to Deactivate Service
Pkg_Manager -> SONATA: Successful Service Deactivation
SONATA -> TMF: Service state INACTIVE
TMF -> "TMF\nDB": Store Service state INACTIVE
TMF -> Web: Service view update
Web -> SvcPrv: Successful service update
```
