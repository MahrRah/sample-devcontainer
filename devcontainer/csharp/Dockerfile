ARG  DOTNET_VERSION="3.1"
FROM mcr.microsoft.com/dotnet/sdk:${DOTNET_VERSION}

RUN useradd -m -s $(which bash) devcont
RUN mkdir /app && chown devcont:devcont /app

USER devcont