FROM microsoft/aspnet:4.7.1 AS runtime

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Download C++ 2012 Redistributable Package (x86)
RUN Invoke-WebRequest http://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe  -OutFile "$env:TEMP\vc2012x86.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2012x86.exe" '/features + /q' -wait

# Download C++ 2013 Redistributable Package (x86)
RUN Invoke-WebRequest http://download.microsoft.com/download/2/E/6/2E61CFA4-993B-4DD4-91DA-3737CD5CD6E3/vcredist_x86.exe  -OutFile "$env:TEMP\vc2013x86.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2013x86.exe" '/features + /q' -wait

# Download C++ 2015 Redistributable Package (x86)
RUN Invoke-WebRequest https://download.microsoft.com/download/6/A/A/6AA4EDFF-645B-48C5-81CC-ED5963AEAD48/vc_redist.x86.exe  -OutFile "$env:TEMP\vc2015x86.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2015x86.exe" '/features + /q' -wait

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
