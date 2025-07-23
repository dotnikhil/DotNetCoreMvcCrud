FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

COPY DotNetCoreMvcCrud.Web/DotNetCoreMvcCrud.Web.csproj 
RUN dotnet restore DotNetCoreMvcCrud.Web/DotNetCoreMvcCrud.Web.csproj

COPY . .
RUN dotnet build DotNetCoreMvcCrud.Web/DotNetCoreMvcCrud.Web.csproj -o ./build

FROM build AS publish
RUN dotnet publish DotNetCoreMvcCrud.Web/DotNetCoreMvcCrud.Web.csproj -c Release -o ./publish /p:UseAppHost=false

From base AS final
COPY --from=publish /src/publish .
ENV ASPNETCORE_URLS=http://*:8081
ENTRYPOINT ["dotnet", "DotNetCoreMvcCrud.Web.dll"]
