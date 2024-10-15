# Use Wolfi base as builder
FROM chainguard/wolfi-base AS builderC
RUN [ `arch` = "aarch64" ] || sleep 1
RUN arch
# Install internally trusted root CAs
RUN apk add --no-cache ca-certificates
RUN update-ca-certificates

# glibc-dynamic is a secure image which can run arbitrary dynamically linked binaries
# Default User - 65532
# Shell - Not Available
# APK - Not Available
FROM chainguard/glibc-dynamic

COPY --from=builderC /etc/ssl/certs /etc/ssl/certs
COPY --from=builderC /usr/local/share/ca-certificates/ /usr/local/share/ca-certificates/

# As Apko Images are Single-Layer, Anchore does not
# detect the USER accurately. Hence we need to set it explicitly
# This should be fixed in Anchore - to use docker inspect properly
USER 65532

