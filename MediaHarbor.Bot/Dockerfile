FROM mcr.microsoft.com/dotnet/aspnet:7.0.13-bullseye-slim-arm64v8 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0.403-bullseye-slim-arm64v8 AS build
WORKDIR /src
COPY ["MediaHarbor.Bot/MediaHarbor.Bot.csproj", "MediaHarbor.Bot/"]
RUN dotnet restore "MediaHarbor.Bot/MediaHarbor.Bot.csproj"
COPY . .
WORKDIR "/src/MediaHarbor.Bot"
RUN dotnet build "MediaHarbor.Bot.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MediaHarbor.Bot.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MediaHarbor.Bot.dll"]
