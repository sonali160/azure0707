FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["azure07/azure07.csproj", "azure07/"]
RUN dotnet restore "azure07/azure07.csproj"
COPY . .
WORKDIR "/src/azure07"
RUN dotnet build "azure07.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "azure07.csproj" -c Release -o /app/publish /p:UseAppHost=false
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "azure07.dll"]



