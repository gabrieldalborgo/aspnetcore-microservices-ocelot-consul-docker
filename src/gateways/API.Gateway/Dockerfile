FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["src/gateways/API.Gateway/API.Gateway.csproj", "src/gateways/API.Gateway/"]
RUN dotnet restore "src/gateways/API.Gateway/API.Gateway.csproj"
COPY . .
WORKDIR "/src/src/gateways/API.Gateway"
RUN dotnet build "API.Gateway.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "API.Gateway.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "API.Gateway.dll"]