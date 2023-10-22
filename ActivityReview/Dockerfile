# Etapa de construcción (build)
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ActivityReview.csproj .
RUN dotnet restore
COPY . .
RUN dotnet build -c Release -o /app/build
RUN dotnet publish -c Release -o /app/publish

COPY appsettings.json /app/publish/appsettings.json

# Etapa de publicación (publish)
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Copiar desde la etapa de construcción a la etapa de publicación
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "ActivityReview.dll"]

