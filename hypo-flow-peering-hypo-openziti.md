```plantuml

' Uncomment this at the end of your design to see only the linked components
hide unlinked

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

PltAdmin -> "Fabric\nController": Issue new account for HypO
"Fabric\nController" -> PltAdmin: HypO account created

== Authenticated peering between HypO and OpenZiti ==

PltAdmin -> Web: Add OpenZiti network
Web -> Fabric: Create network
Fabric -> "Fabric\nController": Authenticate with HypO credentials
"Fabric\nController" -> Fabric: Successful authentication
Fabric -> Web: Network created
Web -> PltAdmin: OpenZiti network added

== Test HypO and OpenZiti interaction ==

PltAdmin -> Web: Create 'test' OpenZiti identity
Web -> Fabric: Create identity
Fabric -> "Fabric\nController": Create identity
"Fabric\nController" -> Fabric: Identity created
Fabric -> Web: Identity created
Web -> PltAdmin: 'test' OpenZiti identity created

```
