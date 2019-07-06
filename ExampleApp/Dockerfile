FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ExampleApp/ExampleApp.csproj ExampleApp/
RUN dotnet restore ExampleApp/ExampleApp.csproj
COPY . .
WORKDIR /src/ExampleApp
RUN dotnet build ExampleApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ExampleApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ExampleApp.dll"]
