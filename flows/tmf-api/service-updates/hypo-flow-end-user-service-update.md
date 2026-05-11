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
SvcPrv -> Web: Authenticate
SvcPrv -> Web: Retrieve Service
Web -> TMF: Submit a Service Package Characteristic Update 
TMF -> "TMF\nDB": Service state update PENDING_UPDATE
TMF -> SONATA: Orchestrate Service Update
SONATA -> Pkg_Manager: Update service deployment
Pkg_Manager -> Compute_Client
Compute_Client -> Pkg_Manager: Successful deployment update
Pkg_Manager -> SONATA
SONATA -> TMF: Complete Service Update
TMF -> "TMF\nDB": Store Previous State and Updated Characteristics
TMF -> Web: Service view update
Web -> SvcPrv: Successful service update
```