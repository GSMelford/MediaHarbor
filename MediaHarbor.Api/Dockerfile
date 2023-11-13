FROM mcr.microsoft.com/dotnet/aspnet:7.0.13-bullseye-slim-arm64v8 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0.403-bullseye-slim-arm64v8 AS build
WORKDIR /src
COPY ["MediaHarbor.Api/MediaHarbor.Api.csproj", "MediaHarbor.Api/"]
RUN dotnet restore "MediaHarbor.Api/MediaHarbor.Api.csproj"
COPY . .
WORKDIR "/src/MediaHarbor.Api"
RUN dotnet build "MediaHarbor.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MediaHarbor.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MediaHarbor.Api.dll"]
