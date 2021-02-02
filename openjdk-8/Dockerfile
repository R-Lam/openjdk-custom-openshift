FROM registry.access.redhat.com/ubi8/openjdk-8
 
USER root
 
RUN microdnf install -y crypto-policies-scripts
 
RUN update-crypto-policies --set LEGACY
 
USER 185