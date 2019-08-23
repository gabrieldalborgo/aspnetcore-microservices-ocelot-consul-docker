FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["src/services/Policies/Policies.csproj", "src/services/Policies/"]
RUN dotnet restore "src/services/Policies/Policies.csproj"
COPY . .
WORKDIR "/src/src/services/Policies"
RUN dotnet build "Policies.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Policies.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Policies.dll"]