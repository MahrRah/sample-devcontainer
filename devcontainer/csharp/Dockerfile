ARG  DOTNET_VERSION="3.1"
FROM mcr.microsoft.com/dotnet/sdk:${DOTNET_VERSION}

RUN useradd -m -s $(which bash) idlab
RUN mkdir /app && chown idlab:idlab /app

USER idlab