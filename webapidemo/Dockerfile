# Use the official .NET SDK image for the build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory
WORKDIR /app

# Copy the csproj and restore the dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application code
COPY . ./

# Build the project
RUN dotnet publish -c Release -o out

# Use the official ASP.NET Runtime image for the final stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# Set the working directory
WORKDIR /app

# Copy the published application from the build stage
COPY --from=build /app/out ./

# Expose the application port (Assuming your API runs on port 80, adjust if needed)
EXPOSE 80

# Set the entry point for the container
ENTRYPOINT ["dotnet", "webapidemo.dll"]
