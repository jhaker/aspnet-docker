FROM microsoft/aspnet:4.7.2 AS runtime

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Download C++ 2017 Redistributable Package (x86)
RUN Invoke-WebRequest https://aka.ms/vs/15/release/vc_redist.x86.exe  -OutFile "$env:TEMP\vc2017x86.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2017x86.exe" '/features + /q' -wait
