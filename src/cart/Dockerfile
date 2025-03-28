# Use the official .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /app

# Copy the project files
COPY src/cart.csproj ./src/
COPY tests/cart.tests.csproj ./tests/

# Restore dependencies
RUN dotnet restore src/cart.csproj

# Copy the remaining files
COPY . .

# Build the application
RUN dotnet build src/cart.csproj --configuration Release --no-restore

# Publish the application
RUN dotnet publish src/cart.csproj -c Release -o /out --no-restore

# Use the official runtime image to run the app
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app

# Copy the built application
COPY --from=build /out .

# Set the entry point
ENTRYPOINT ["dotnet", "cart.dll"]

# Expose the necessary ports
EXPOSE 5000
