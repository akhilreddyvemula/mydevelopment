# Use the .NET SDK image to build your app
FROM mcr.microsoft.com/dotnet/sdk:8.0-nanoserver-1809 AS build

# Set the working directory inside the container
WORKDIR /src

# Copy the project file(s)
COPY ["matermindcentific.csproj", "./"]

# Set the user to Administrator to ensure sufficient permissions for restore
USER ContainerAdministrator

# Restore the dependencies
RUN dotnet restore "./matermindcentific.csproj"

# Copy the remaining files
COPY . .

# Build the application
WORKDIR "/src/matermindcentific"
RUN dotnet build "./matermindcentific.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "./matermindcentific.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Use the ASP.NET runtime image to run the application
FROM mcr.microsoft.com/dotnet/aspnet:8.0-nanoserver-1809 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "matermindcentific.dll"]
