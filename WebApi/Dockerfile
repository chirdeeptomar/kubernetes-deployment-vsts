FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 63537
EXPOSE 44369

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY WebApi/WebApi.csproj WebApi/
RUN dotnet restore WebApi/WebApi.csproj
COPY . .
WORKDIR /src/WebApi
RUN dotnet build WebApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApi.dll"]
