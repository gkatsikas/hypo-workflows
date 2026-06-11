```plantuml

hide unlinked

!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/palette/hypo-palette.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/theme/hypo-theme.puml
!includeurl https://raw.githubusercontent.com/gkatsikas/hypo-workflows/refs/heads/main/components/hypo-components.puml

' All sections begin with: POST /v1/auth/jwt/login {role:"default", jwt:<bearer>} → client token

== Store Kubernetes config ==

Registry -> "Secrets\nDB": POST /v1/secret/data/hypo/kubernetes-config/<group>/{serviceId}

== Retrieve Kubernetes config ==

Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/kubernetes-config/<group>/{serviceId}

== Retrieve package registry credentials (type="parsing") ==

opt#White #Gold OCM deployment
    Registry -> "Secrets\nDB": PUT /v1/secret/data/hypo/service-order/<group>/{serviceId}
end
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/package-registry/<group>/{sanitizedUrl}

== Retrieve deployment config (type="deployment") ==

Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/kubernetes-config/<group>/{clusterID}
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/service-order/<group>/{serviceId}
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/image-pull/<group>/{secretName} ×N

== Retrieve activation config (type="activation") ==

Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/kubernetes-config/<group>/{clusterID}
Registry -> "Secrets\nDB": GET /v1/secret/data/hypo/service-order/<group>/{serviceId}

== Persist Fabric credentials ==

Registry -> "Secrets\nDB": POST /v1/secret/data/hypo/fabric-secret/<group>/{networkControllerId}

== Delete Fabric credentials ==

Registry -> "Secrets\nDB": DELETE /v1/secret/data/hypo/fabric-secret/<group>/{networkControllerId}

```
