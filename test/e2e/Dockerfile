FROM registry.ci.openshift.org/openshift/release:rhel-8-release-golang-1.23-openshift-4.19 as builder
WORKDIR /go/src/github.com/openshift/managed-cluster-validating-webhooks
COPY . .
RUN  CGO_ENABLED=0 GOFLAGS="-mod=mod" go test ./test/e2e -v -c --tags=osde2e -o /harness.test

FROM registry.access.redhat.com/ubi8/ubi-minimal:latest
COPY --from=builder ./harness.test harness.test
ENTRYPOINT [ "/harness.test" ]