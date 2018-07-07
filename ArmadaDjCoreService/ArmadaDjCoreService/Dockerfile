FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 6554
EXPOSE 44398

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ArmadaDjCoreService/ArmadaDjCoreService.csproj ArmadaDjCoreService/
RUN dotnet restore ArmadaDjCoreService/ArmadaDjCoreService.csproj
COPY . .
WORKDIR /src/ArmadaDjCoreService
RUN dotnet build ArmadaDjCoreService.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ArmadaDjCoreService.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ArmadaDjCoreService.dll"]
