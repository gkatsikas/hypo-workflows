```plantuml

!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' =====================
' Example Flow
' =====================
SvcPrv -> Web: Service order configuration
SvcPrv -> Web: Service order request
Web -> TMF : Request Service
TMF -> SONATA : Orchestrate
SONATA -> Pkg_Manager : Deploy Package
Pkg_Manager -> Telemetry_Client : Send Metrics
Telemetry_Client -> Registry : Register Data
Registry -> OSS_Client : Notify Update
Fabric -> "Fabric\nController" : Bla
Web -> SvcPrv: Service order completed

```
