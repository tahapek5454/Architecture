#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/runtime:9.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["AuditLogWorkerService/AuditLogWorkerService.csproj", "AuditLogWorkerService/"]
RUN dotnet restore "AuditLogWorkerService/AuditLogWorkerService.csproj"
COPY . .
WORKDIR "/src/AuditLogWorkerService"
RUN dotnet build "AuditLogWorkerService.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AuditLogWorkerService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AuditLogWorkerService.dll"]