FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["NG.Host.WebApi/NG.Host.WebApi.csproj", "NG.Host.WebApi/"]
RUN dotnet restore "NG.Host.WebApi/NG.Host.WebApi.csproj"
COPY . .
WORKDIR "/src/NG.Host.WebApi"
RUN dotnet build "NG.Host.WebApi.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "NG.Host.WebApi.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NG.Host.WebApi.dll"]
