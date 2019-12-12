# Building an image - `docker build --pull -t viewer:examples .`
# Running a container - `docker run --rm -it -v ${PWD}:/examples/results viewer:examples`
 
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS buid_env

# prepare
WORKDIR /examples
COPY ./*.sln ./
COPY ./GroupDocs.Viewer.Examples.CSharp/ ./GroupDocs.Viewer.Examples.CSharp/
COPY ./GroupDocs.Viewer.Examples.CSharp.Core/ ./GroupDocs.Viewer.Examples.CSharp.Core/
# end prepare

# GroupDocs.Viewer dependency - https://docs.groupdocs.com/display/viewernet/.NET+Standard+2.0+API+Limitations
RUN dotnet add ./GroupDocs.Viewer.Examples.CSharp.Core/GroupDocs.Viewer.Examples.CSharp.Core.csproj package SkiaSharp.NativeAssets.Linux --framework netcoreapp3.1
# GroupDocs.Viewer dependency

# restore
WORKDIR /examples
RUN dotnet restore ./GroupDocs.Viewer.Examples.CSharp.Core/GroupDocs.Viewer.Examples.CSharp.Core.csproj
# end restore

## build
WORKDIR /examples
## end build
RUN dotnet publish ./GroupDocs.Viewer.Examples.CSharp.Core/GroupDocs.Viewer.Examples.CSharp.Core.csproj --no-restore --framework netcoreapp3.1 --configuration Debug -o ./output

FROM mcr.microsoft.com/dotnet/core/runtime:3.1 

# begin GroupDocs.Viewer dependencies - https://docs.groupdocs.com/display/viewernet/.NET+Standard+2.0+API+Limitations
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y libgdiplus \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y libc6-dev

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y libfontconfig1 \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y xfonts-utils

RUN echo "deb http://httpredir.debian.org/debian jessie main contrib" > /etc/apt/sources.list \
    && echo "deb http://security.debian.org/ jessie/updates main contrib" >> /etc/apt/sources.list \
    && echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y ttf-mscorefonts-installer \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*
# end GroupDocs.Viewer dependencies

WORKDIR /examples
COPY --from=buid_env /examples/output .
ENTRYPOINT ["dotnet", "GroupDocs.Viewer.Examples.CSharp.Core.dll"]