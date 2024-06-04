FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["CRUDAPI/CRUDAPI.csproj", "CRUDAPI/"]
RUN dotnet restore "CRUDAPI/CRUDAPI.csproj"
COPY . .
WORKDIR "/src/CRUDAPI"
RUN dotnet build "CRUDAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CRUDAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CRUDAPI.dll"]
