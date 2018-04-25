FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY WebApplication7.sln ./
COPY WebApplication7/WebApplication7.csproj WebApplication7/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/WebApplication7
RUN dotnet build WebApplication7.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplication7.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication7.dll"]
