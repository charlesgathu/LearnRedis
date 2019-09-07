FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ListenerApp/ListenerApp.csproj", "ListenerApp/"]
RUN dotnet restore "ListenerApp/ListenerApp.csproj"
COPY . .
WORKDIR "/src/ListenerApp"
RUN dotnet build "ListenerApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ListenerApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ListenerApp.dll"]
