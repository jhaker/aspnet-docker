FROM microsoft/aspnet:4.7.2 AS runtime

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# Download C++ 2012 Redistributable Package (x64)
RUN Invoke-WebRequest http://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe  -OutFile "$env:TEMP\vc2012x64.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2012x64.exe" '/features + /q' -wait

# Download C++ 2013 Redistributable Package (x64)
RUN Invoke-WebRequest http://download.microsoft.com/download/2/E/6/2E61CFA4-993B-4DD4-91DA-3737CD5CD6E3/vcredist_x64.exe  -OutFile "$env:TEMP\vc2013x64.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2013x64.exe" '/features + /q' -wait

# Download C++ 2015 Redistributable Package (x64)
RUN Invoke-WebRequest https://download.microsoft.com/download/6/A/A/6AA4EDFF-645B-48C5-81CC-ED5963AEAD48/vc_redist.x64.exe  -OutFile "$env:TEMP\vc2015x64.exe" -UseBasicParsing  
RUN Start-Process "$env:TEMP\vc2015x64.exe" '/features + /q' -wait

