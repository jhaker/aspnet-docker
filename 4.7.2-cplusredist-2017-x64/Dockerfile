FROM microsoft/aspnet:4.7.2 AS runtime

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Download C++ 2017 Redistributable Package (x64)
RUN Invoke-WebRequest https://aka.ms/vs/15/release/vc_redist.x64.exe  -OutFile "$env:TEMP\vc2017x64.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2017x64.exe" '/features + /q' -wait

# Install iis manager
RUN wget https://download.microsoft.com/download/1/2/8/128E2E22-C1B9-44A4-BE2A-5859ED1D4592/rewrite_amd64_en-US.msi -OutFile rewrite_amd64_en-US.msi; msiexec /i "rewrite_amd64_en-US.msi" /q /log foo.log; \
	Import-Module -Name WebAdministration; \
	Import-Module -Name IISAdministration; \
	Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force; \
	Install-Module -Name IISAdministration -Force; \
	Install-Module -Name IISAdministration -RequiredVersion 1.1.0.0 -Force;  \
	Remove-Module IISAdministration; \
	Get-IISServerManager;

# Remove default web site
RUN Remove-Website 'Default Web Site'; 
