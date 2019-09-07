FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Aggregator/Aggregator.csproj", "Aggregator/"]
RUN dotnet restore "Aggregator/Aggregator.csproj"
COPY . .
WORKDIR "/src/Aggregator"
RUN dotnet build "Aggregator.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Aggregator.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Aggregator.dll"]
