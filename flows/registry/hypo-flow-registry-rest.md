```plantuml

hide unlinked

!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' All sections begin with: POST /v1/auth/jwt/login {role:"default", jwt:<bearer>} → client token

== package-registry / image-pull — secret CRUD ==

Registry -> "Secrets\nDB": POST /v1/secret/data/hypo/<type>/<group>/{name}
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/<type>/<group>/{name}
Registry -> "Secrets\nDB": PUT /v1/secret/data/hypo/<type>/<group>/{name}
Registry -> "Secrets\nDB": DELETE /v1/secret/data/hypo/<type>/<group>/{name}
"Secrets\nDB" -> Registry: stored / data / updated / deleted

== package-registry / image-pull — list ==

Registry -> "Secrets\nDB": GET /v1/secret/metadata/hypo/<type>/<group>?list=true
"Secrets\nDB" -> Registry: key list
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/<type>/<group>/{key} ×N
"Secrets\nDB" -> Registry: secret data

== Kubernetes configs — list ==

Registry -> "Secrets\nDB": GET /v1/secret/metadata/hypo/kubernetes-config/<group>?list=true
"Secrets\nDB" -> Registry: key list
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/kubernetes-config/<group>/{key} ×N
"Secrets\nDB" -> Registry: config data

== Kubernetes config — terminal token ==

Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/kubernetes-config/<group>/{serviceId}
"Secrets\nDB" -> Registry: kubeconfig data

== Policy CRUD ==

Registry -> "Secrets\nDB": POST /v1/sys/policy/{name}
Registry -> "Secrets\nDB": GET /v1/sys/policy/{name}
Registry -> "Secrets\nDB": PUT /v1/sys/policy/{name}
Registry -> "Secrets\nDB": DELETE /v1/sys/policy/{name}
"Secrets\nDB" -> Registry: created / data / updated / deleted

== Group CRUD ==

Registry -> "Secrets\nDB": POST /v1/identity/group
Registry -> "Secrets\nDB": GET /v1/identity/group/name/{name}
Registry -> "Secrets\nDB": PUT /v1/identity/group/name/{name}
Registry -> "Secrets\nDB": DELETE /v1/identity/group/name/{name}
"Secrets\nDB" -> Registry: created / data / updated / deleted

```
