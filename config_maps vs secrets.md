In Kubernetes, Secrets and ConfigMaps are used to manage configuration data for applications. They share similarities but are designed for different purposes, particularly around sensitive data.

ConfigMap

	•	Purpose: Store non-sensitive configuration data as key-value pairs.
	•	Use Cases:
	•	Application settings
	•	Environment variables
	•	Configuration files
	•	Command-line arguments
	•	Features:
	•	Data is not encrypted (stored as plain text in etcd).
	•	Can be used to decouple configuration artifacts from application code.
	•	Can hold a small amount of data or configuration (less than 1MB).
	•	Example YAML:

apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DATABASE_URL: "mysql://user@localhost:3306/mydb"
  APP_MODE: "production"

	•	Usage in a Pod:
	•	As environment variables:

envFrom:
  - configMapRef:
      name: app-config


	•	As a mounted file:

volumeMounts:
  - name: config-volume
    mountPath: /etc/config
volumes:
  - name: config-volume
    configMap:
      name: app-config

Secrets

	•	Purpose: Store sensitive data, such as passwords, API keys, or certificates.
	•	Use Cases:
	•	Database credentials
	•	TLS certificates
	•	Sensitive application configurations
	•	Features:
	•	Data is encoded using Base64 (not encrypted by default).
	•	Can be encrypted at rest in etcd (enable encryption for better security).
	•	Access can be controlled using RBAC.
	•	Similar usage patterns as ConfigMap but designed for sensitive data.
	•	Example YAML:

apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  DB_PASSWORD: cGFzc3dvcmQ=  # Base64 encoded value of "password"

	•	Usage in a Pod:
	•	As environment variables:

env:
  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: app-secret
        key: DB_PASSWORD


	•	As a mounted file:

volumeMounts:
  - name: secret-volume
    mountPath: /etc/secret
volumes:
  - name: secret-volume
    secret:
      secretName: app-secret

Key Differences

Aspect	ConfigMap	Secret
Purpose	Non-sensitive configuration data	Sensitive data like credentials
Storage	Plain text in etcd	Base64 encoded (optionally encrypted)
Access	General-purpose data	Controlled access with RBAC
Security	No encryption	Supports encryption at rest
Size Limit	1MB	1MB

Best Practices

	1.	Separate Secrets and Configurations: Avoid mixing sensitive and non-sensitive data for better security management.
	2.	Use Encryption: Enable etcd encryption for Secrets to ensure sensitive data is secure.
	3.	Access Control: Use RBAC to control who can access Secrets and ConfigMaps.
	4.	Avoid Hardcoding: Do not hardcode sensitive or configuration data directly in your application code.
	5.	Regular Updates: Rotate Secrets regularly to minimize the risk of exposure.