
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY TestDemoApp.csproj .
RUN dotnet restore "TestDemoApp.csproj"
COPY . .
RUN dotnet build "TestDemoApp.csproj" -c Release -o /build
RUN dotnet publish "TestDemoApp.csproj" -c Release -o /publish 

FROM build AS final
WORKDIR /app
COPY --from=publish /publish .
ENTRYPOINT ["dotnet", "TestDemoApp.dll"]
