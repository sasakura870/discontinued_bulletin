#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["discontinued_bulletin/discontinued_bulletin.csproj", "discontinued_bulletin/"]
RUN dotnet restore "discontinued_bulletin/discontinued_bulletin.csproj"
COPY . .
WORKDIR "/src/discontinued_bulletin"
RUN dotnet build "discontinued_bulletin.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "discontinued_bulletin.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "discontinued_bulletin.dll"]