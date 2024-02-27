# Get Base SDK Image from Microsoft
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Copy the.CsPROJ file and restore any dependencies (via NUGET)
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY *.csproj ./
RUN dotnet restore 

# Copy the project files and Build our release
COPY . ./
RUN dotnet build -c Release -o out 

# Genertae runtime Image
FROM build AS publish
RUN dotnet publish -c Release -o out /p:UseAppHost=false


FROM base AS final
WORKDIR /app
COPY --from=publish /app/out .
ENTRYPOINT ["dotnet", "TestDemoApp.dll"]
