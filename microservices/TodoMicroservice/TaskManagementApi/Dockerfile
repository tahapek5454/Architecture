#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["TaskManagementApi/TaskManagementApi.csproj", "TaskManagementApi/"]
RUN dotnet restore "TaskManagementApi/TaskManagementApi.csproj"
COPY . .
WORKDIR "/src/TaskManagementApi"
RUN dotnet build "TaskManagementApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TaskManagementApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "TaskManagementApi.dll"]