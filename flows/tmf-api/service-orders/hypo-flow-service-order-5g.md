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

SvcPrv -> Web: Add 5G service specification into shopping cart
SvcPrv -> Web: Configure service characteristics
SvcPrv -> Web: Place service order
Web -> TMF: Dispatch service order
TMF -> "TMF\nDB": Store service order
TMF -> SONATA: Orchestrate service order
SONATA -> OSS_Client: Order 5G from OpenSlice
OSS_Client -> "ETSI\nOpenSlice"
"ETSI\nOpenSlice" -> "5G\nSystem": Deploy
"5G\nSystem" -> "ETSI\nOpenSlice": Successful 5G deployment
"ETSI\nOpenSlice" -> OSS_Client
OSS_Client -> SONATA: Successful 5G service order
SONATA -> TMF: Service state ACTIVE
SONATA -> TMF: Service order state COMPLETED
TMF -> Web: Service order view update
Web -> SvcPrv: Successful 5G service order
```
