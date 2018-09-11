FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 64259
EXPOSE 44394

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY SimpleDockerExample/SimpleDockerExample.csproj SimpleDockerExample/
RUN dotnet restore SimpleDockerExample/SimpleDockerExample.csproj
COPY . .
WORKDIR /src/SimpleDockerExample
RUN dotnet build SimpleDockerExample.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SimpleDockerExample.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SimpleDockerExample.dll"]
