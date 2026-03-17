```plantuml

' Uncomment this at the end of your design to see only the linked components
' hide unlinked

' General templates useful for every workflow
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml

' Define the stakeholders of this workflow
actor "Platform\nAdmin" as PltAdmin #000000

' General template providing the ETSI HypO components
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' SvcPrv -> Web: Service order configuration
' SvcPrv -> Web: Service order request
' Web -> TMF : Request Service
' TMF -> SONATA : Orchestrate
' SONATA -> Pkg_Manager : Deploy Package
' Pkg_Manager -> Telemetry_Client : Send Metrics
' Telemetry_Client -> Registry : Register Data
' Registry -> OSS_Client : Notify Update
' Fabric -> "Fabric\nController" : Bla
' Web -> SvcPrv: Service order completed

' =====================
' Peering Flow between
' HypO and OpenZiti
' =====================

== Create HypO account on OpenZiti ==

PltAdmin -> "Fabric\nController": Issue new account for ESO
"Fabric\nController" -> PltAdmin: ESO account created

' == Authenticated peering between ESO and OpenZiti ==

' PltAdmin -> "ESO\nPortal": Add OpenZiti network
' "ESO\nPortal" -> "ESO\nBackend": Create network
' "ESO\nBackend" -> "Fabric\nController": Authenticate with ESO credentials
' "Fabric\nController" -> "ESO\nBackend": Successful authentication
' "ESO\nBackend" -> "ESO\nPortal": Network created
' "ESO\nPortal" -> PltAdmin: OpenZiti network added

' == Test HypO and OpenZiti interaction ==

' PltAdmin -> "ESO\nPortal": Create test OpenZiti identity
' "ESO\nPortal" -> "ESO\nBackend": Create identity
' "ESO\nBackend" -> "Fabric\nController": Create identity
' "Fabric\nController" -> "ESO\nBackend": Identity created
' "ESO\nBackend" -> "ESO\nPortal": Identity created
' "ESO\nPortal" -> PltAdmin: Test OpenZiti identity created

```
