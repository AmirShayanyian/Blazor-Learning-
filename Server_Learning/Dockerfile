FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Server_Learning/Server_Learning.csproj", "Server_Learning/"]
RUN dotnet restore "Server_Learning/Server_Learning.csproj"
COPY . .
WORKDIR "/src/Server_Learning"
RUN dotnet build "Server_Learning.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Server_Learning.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Server_Learning.dll"]
