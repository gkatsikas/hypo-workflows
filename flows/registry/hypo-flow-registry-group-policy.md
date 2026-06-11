```plantuml

hide unlinked

!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

participant "HashiCorp\nVault" as Vault

' All sections begin with: POST /v1/auth/jwt/login {role:"default", jwt:<bearer>} → client token

== Vault group policy provisioning ==

Registry -> Vault: POST /v1/sys/policy/{groupName}_policy\nCRUD on secret/data/hypo/*/{groupName}/

Registry -> Vault: POST /v1/identity/group\nname={groupName}, type=external, policies=[{groupName}_policy]

alt#White #Gold Group created
else Group creation failed — rollback
    Registry -> Vault: DELETE /v1/sys/policy/{groupName}_policy
end

```
