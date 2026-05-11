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
' 5G Service Order
' =====================

== 5G Service Order Flow ==

SvcPrv -> Web: Authenticate
SvcPrv -> Web: Add 5G service specification into shopping cart
SvcPrv -> Web: Configure service characteristics
SvcPrv -> Web: Place service order
Web -> TMF: Dispatch service order
TMF -> "TMF\nDB": Store Service Order
TMF -> SONATA: Orchestrate Service Order
SONATA -> OSS_Client: Order 5G from OpenSlice
OSS_Client -> "ETSI\nOpenSlice"
OSS_Client -> SONATA: Order Success
SONATA -> TMF: Service state ACTIVE
SONATA -> TMF: Service order state COMPLETED
TMF -> Web: Service order view update
Web -> SvcPrv: Successful service order
```
