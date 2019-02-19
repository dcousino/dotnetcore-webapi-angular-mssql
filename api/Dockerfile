FROM microsoft/dotnet:2.1.2-aspnetcore-runtime-alpine AS base
WORKDIR /app
#EXPOSE 57270
#EXPOSE 44348
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-alpine3.8 AS build
WORKDIR /src
COPY api.csproj .
RUN dotnet restore
COPY . .
WORKDIR /src
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "api.dll"]
