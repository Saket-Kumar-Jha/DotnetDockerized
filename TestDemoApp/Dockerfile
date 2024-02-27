# Get Base SDK Image from Microsoft
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy the.CsPROJ file and restore any dependencies (via NUGET)
COPY *.csproj ./
RUN dotnet restore 

# Copy the project files and Build our release
COPY . ./
RUN dotnet publish -c Release -o out 

# Genertae runtime Image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS final
WORKDIR /app
Expose 5000
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "TestDemoApp.dll"]
