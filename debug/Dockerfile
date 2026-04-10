# FROM almalinux:9
# RUN dnf install telnet iputils net-tools bind-utils -y
# #CMD ["sleep", "2000"]
# CMD ["sleep", "20000"]
#--------------------------------------------------------#
# Stage 1: Build stage (has package manager)
FROM almalinux:9-minimal AS builder
RUN microdnf install telnet iputils net-tools bind-utils -y

# Stage 2: Final tiny image (no package manager)
FROM almalinux/9-micro:latest
WORKDIR /app

# Copy the binaries you need
COPY --from=builder /usr/bin/telnet /usr/bin/ping /usr/bin/netstat /usr/bin/dig /usr/bin/
# Copy the required shared libraries (important for the tools to run)
COPY --from=builder /usr/lib64/ /usr/lib64/

CMD ["sleep", "20000"]