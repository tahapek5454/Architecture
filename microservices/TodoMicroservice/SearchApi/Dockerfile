#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["SearchApi/SearchApi.csproj", "SearchApi/"]
RUN dotnet restore "SearchApi/SearchApi.csproj"
COPY . .
WORKDIR "/src/SearchApi"
RUN dotnet build "SearchApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SearchApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SearchApi.dll"]