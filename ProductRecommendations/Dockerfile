# Pull the base image
FROM microsoft/dotnet:2.1-sdk AS build
LABEL maintainer="jay.bisa@gmail.com"
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore ProductRecommendations.csproj

# Copy everything else and build
COPY . ./
RUN dotnet publish ProductRecommendations.csproj -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime AS runtime
WORKDIR /app
COPY --from=build /app/out .
ENTRYPOINT ["dotnet", "ProductRecommendations.dll"]