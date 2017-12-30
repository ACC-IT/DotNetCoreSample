FROM microsoft/dotnet:2.0-runtime-nanoserver-sac2016 AS base
WORKDIR /app

FROM microsoft/dotnet:2.0-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY *.sln ./
COPY DotNetCoreSample/DotNetCoreSample.csproj DotNetCoreSample/
RUN dotnet restore
COPY . .
WORKDIR /src/DotNetCoreSample
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DotNetCoreSample.dll"]
