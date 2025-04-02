# =========================
# 🛠 Stage 1: Setup Base Layer
# =========================
FROM ubuntu:22.04 AS base

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update &&     apt-get install -y wget curl gnupg2 ca-certificates openjdk-17-jdk &&     apt-get clean &&     rm -rf /var/lib/apt/lists/*

# Create required directory structure
RUN mkdir -p /jfrog/artifactory/var/etc /jfrog/artifactory/var/log /jfrog/artifactory/var/data

# =========================
# 🐳 Stage 2: Final Image from JFrog
# =========================
FROM releases-docker.jfrog.io/jfrog/artifactory-oss:latest

# Copy dependencies and custom dirs from base image
COPY --from=base /jfrog /jfrog
COPY --from=base /usr/lib/jvm /usr/lib/jvm

# Expose default ports
EXPOSE 8081 8082

# Entrypoint already defined by original JFrog image
# CMD is also handled by base image so no override needed
