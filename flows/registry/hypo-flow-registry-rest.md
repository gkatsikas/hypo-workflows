```plantuml

hide unlinked

!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

participant "HashiCorp\nVault" as Vault

' All sections begin with: POST /v1/auth/jwt/login {role:"default", jwt:<bearer>} → client token

== package-registry / image-pull — secret CRUD ==

Registry -> Vault: POST /v1/secret/data/hypo/<type>/<group>/{name}
Registry -> Vault: GET /v1/secret/data/hypo/<type>/<group>/{name}
Registry -> Vault: PUT /v1/secret/data/hypo/<type>/<group>/{name}
Registry -> Vault: DELETE /v1/secret/data/hypo/<type>/<group>/{name}
Vault -> Registry: stored / data / updated / deleted

== package-registry / image-pull — list ==

Registry -> Vault: GET /v1/secret/metadata/hypo/<type>/<group>?list=true
Vault -> Registry: key list
Registry -> Vault: GET /v1/secret/data/hypo/<type>/<group>/{key} ×N
Vault -> Registry: secret data

== Kubernetes configs — list ==

Registry -> Vault: GET /v1/secret/metadata/hypo/kubernetes-config/<group>?list=true
Vault -> Registry: key list
Registry -> Vault: GET /v1/secret/data/hypo/kubernetes-config/<group>/{key} ×N
Vault -> Registry: config data

== Kubernetes config — terminal token ==

Registry -> Vault: GET /v1/secret/data/hypo/kubernetes-config/<group>/{serviceId}
Vault -> Registry: kubeconfig data

== Policy CRUD ==

Registry -> Vault: POST /v1/sys/policy/{name}
Registry -> Vault: GET /v1/sys/policy/{name}
Registry -> Vault: PUT /v1/sys/policy/{name}
Registry -> Vault: DELETE /v1/sys/policy/{name}
Vault -> Registry: created / data / updated / deleted

== Group CRUD ==

Registry -> Vault: POST /v1/identity/group
Registry -> Vault: GET /v1/identity/group/name/{name}
Registry -> Vault: PUT /v1/identity/group/name/{name}
Registry -> Vault: DELETE /v1/identity/group/name/{name}
Vault -> Registry: created / data / updated / deleted

```
