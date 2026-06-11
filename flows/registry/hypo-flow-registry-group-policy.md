```plantuml

hide unlinked

!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' All sections begin with: POST /v1/auth/jwt/login {role:"default", jwt:<bearer>} → client token

== Secret group policy provisioning ==

Registry -> "Secrets\nDB": POST /v1/sys/policy/{groupName}_policy\nCRUD on secret/data/hypo/*/{groupName}/

Registry -> "Secrets\nDB": POST /v1/identity/group\nname={groupName}, type=external, policies=[{groupName}_policy]

alt#White #Gold Group created
    note over Registry, "Secrets\nDB": Successful group secret storage
else Group creation failed — rollback
    Registry -> "Secrets\nDB": DELETE /v1/sys/policy/{groupName}_policy
end

```
