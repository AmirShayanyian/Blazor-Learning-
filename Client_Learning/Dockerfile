FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Client_Learning/Client_Learning.csproj", "Client_Learning/"]
RUN dotnet restore "Client_Learning/Client_Learning.csproj"
COPY . .
WORKDIR "/src/Client_Learning"
RUN dotnet build "Client_Learning.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Client_Learning.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Client_Learning.dll"]
