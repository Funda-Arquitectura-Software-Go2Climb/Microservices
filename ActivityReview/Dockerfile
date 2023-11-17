﻿FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["ActivityReview/ActivityReview.csproj", "ActivityReview/"]
RUN dotnet restore "ActivityReview/ActivityReview.csproj"
COPY . .
WORKDIR "/src/ActivityReview"
RUN dotnet build "ActivityReview.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ActivityReview.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ActivityReview.dll"]