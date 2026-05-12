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

' =====================
' Peering Flow between
' ETSI HypO and ETSI OpenSlice
' =====================

== Peering preparation: Reflect remote OSS as a TMF Party Organization ==

PltAdmin -> Web: Fill in peering information
Web -> TMF: Create an organization party
TMF -> "TMF\nDB": Store organization party
"TMF\nDB" -> TMF: Organization party stored
TMF -> Web: Party created
Web -> Peering: Send organization party information

== Peering initiation: Pull services from remote OSS ==

Peering -> "ETSI\nOpenSlice": Retrieve service specifications
Peering -> Web: Service specifications retrieved
Web -> Peering: Admin chooses the service specifications to import into HypO's catalog(s)
Peering -> "ETSI\nOpenSlice": Request service specification details
"ETSI\nOpenSlice" -> Peering: Service specification details retrieved

== Peering persistence: Store remote OSS services locally ==

Peering -> "Service\nBus": Dispatch service specification details to database
"Service\nBus" -> TMF: Service specification details dispatched
TMF -> "TMF\nDB": Store service specification details
"TMF\nDB" -> TMF: Service specification details stored

== Peering conclusion: Expose remote OSS services through Marketplace ==

Peering -> Web: Peering successfully concluded
Web -> PltAdmin: Remote OSS service specifications in Marketplace

== Periodic peering check ==

loop every 5 minutes
Peering -> "ETSI\nOpenSlice": Request service specification details
"ETSI\nOpenSlice" -> Peering: Service specification details retrieved
end


```
