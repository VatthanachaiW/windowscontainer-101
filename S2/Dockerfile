# Set base image to publish source code
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8 AS build
# Set work directory
WORKDIR /app   
# Copy solution file to work directory
COPY ["HelloWorld-MVC.sln","."]
# Copy project to work directory
COPY ["HelloWorld-MVC/", "HelloWorld-MVC/"]
# Restore nuget package
RUN nuget restore
# publish project and set output to /app/publish
RUN msbuild HelloWorld-MVC/HelloWorld-MVC.csproj /p:Configuration=Release

# Set base image to run
FROM mcr.microsoft.com/dotnet/framework/aspnet:4.8 AS runtime
# Set direcory to deploy publish project
WORKDIR /inetpub/wwwroot
# Copy publish project from previous stage
COPY --from=build /app/HelloWorld-MVC/. .