FROM quay.io/openshift/origin-operator-registry:latest

ARG FULL_OPERATOR_IMAGE

COPY deploy/olm-catalog /registry/performance-addon-operator-catalog

# replaces performance-addon-operator image with the one matching our build
RUN find /registry/performance-addon-operator-catalog/ -type f -exec sed -i "s|REPLACE_IMAGE|${FULL_OPERATOR_IMAGE}|g" {} \; || :

# Initialize the database
RUN initializer --manifests /registry/performance-addon-operator-catalog --output bundles.db

# There are multiple binaries in the origin-operator-registry
# We want the registry-server
ENTRYPOINT ["registry-server"]
CMD ["--database", "bundles.db"]
