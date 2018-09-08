FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["demoapp/demoapp.csproj", "demoapp/"]
RUN dotnet restore "demoapp/demoapp.csproj"
COPY . .
WORKDIR "/src/demoapp"
RUN dotnet build "demoapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "demoapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "demoapp.dll"]