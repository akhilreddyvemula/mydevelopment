
# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copy the project file(s) and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application and publish it
COPY ./ ./
RUN dotnet publish -c Release -o out

# Stage 2: Serve
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Copy the published output from the build stage
COPY --from=build-env /app/out ./

# Set the entry point for the application
ENTRYPOINT ["dotnet", "matermindcentific.dll"]

