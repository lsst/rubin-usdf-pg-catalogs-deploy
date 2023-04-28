
SECRET_PATH ?= secret/rubin/usdf-pg-catalogs/dp03-postgres
S3_SECRET_PATH ?= secret/rubin/usdf-pg-catalogs/dp03-s3

get-secrets-from-vault:
	mkdir -p etc/.secrets/
	set -e; for i in username password client-id client-secret; do vault kv get --field=$$i $(SECRET_PATH) > etc/.secrets/$$i ; done

clean-secrets:
	rm -rf etc/.secrets/

run-apply:
	kubectl apply -k .

run-kustomize:
	kubectl kustomize .

patch-poolers:
	kubectl apply -f endpoints-patch.yaml

dump: get-secrets-from-vault run-kustomize clean-secrets

apply: get-secrets-from-vault run-apply clean-secrets


