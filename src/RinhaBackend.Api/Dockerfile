﻿FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["src/RinhaBackend.Api/RinhaBackend.Api.csproj", "src/RinhaBackend.Api/"]
RUN dotnet restore "src/RinhaBackend.Api/RinhaBackend.Api.csproj"
COPY . .
WORKDIR "/src/src/RinhaBackend.Api"
RUN dotnet build "RinhaBackend.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RinhaBackend.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RinhaBackend.Api.dll"]
