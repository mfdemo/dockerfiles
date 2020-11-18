#
# Windows Nano Server 1809 (with PowerShell) - Open JDK 1.8.0
#

FROM mcr.microsoft.com/powershell:lts-nanoserver-1809

MAINTAINER Kevin A. Lee <kevin.lee@microfocus.com>

# Java version and checksum for downloaded version from https://github.com/ojdkbuild
ARG JAVA_VERSION=java-1.8.0-openjdk-1.8.0.252-2.b09
ARG JAVA_SHA256=7cb99dc5e6a79e8ffc893e9a84ec57bbff2e4612873feeed039dc2d631a0e019

# Environment variables to set (current user)
ENV JAVA_VERSION=${JAVA_VERSION}
ENV JAVA_SHA256=${JAVA_SHA256}
ENV JAVA_HOME="C:\\openjdk\\${JAVA_BUILD_VERSION}"

# Run as ContainerAdministrator in order to set system environment variables
USER ContainerAdministrator

# Set as system environment variables (all users)
RUN setx /M JAVA_HOME ${JAVA_HOME}
RUN setx /M PATH "%PATH%;%JAVA_HOME%\bin"

# Powershell script to download OpenJDK Zip file and extract\expand to C:\openjdk
RUN pwsh -Command [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 ; \
    Invoke-WebRequest $('https://github.com/ojdkbuild/ojdkbuild/releases/download/{0}/{0}.ojdkbuild.windows.x86_64.zip' -f $env:JAVA_VERSION) -OutFile 'openjdk.zip' -UseBasicParsing ; \
    if ((Get-FileHash openjdk.zip -Algorithm sha256).Hash -ne $env:JAVA_SHA256) {exit 1} ; \
    Expand-Archive openjdk.zip -DestinationPath "C:\\" ; \
	Rename-Item $('{0}.ojdkbuild.windows.x86_64' -f $env:JAVA_VERSION) C:\\openjdk ; \
    Remove-Item -Path openjdk.zip
	
# Run anything as as ContainerUser
#USER ContainerUser	

# Entrypoint is default (Powershell)
