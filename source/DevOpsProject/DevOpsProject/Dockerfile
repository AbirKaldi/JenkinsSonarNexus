# Stage 1: Build stage
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS base
WORKDIR /app
EXPOSE 5000
ENV ASPNETCORE_URLS=http://+:5000

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["DevOpsProject.csproj", "./"]
RUN dotnet restore "DevOpsProject.csproj"
COPY . .
RUN dotnet build "DevOpsProject.csproj" -c Release -o /app/build

# Stage 2: Publish stage
FROM build AS publish
RUN dotnet publish "DevOpsProject.csproj" -c Release -o /app/publish  # Corrected command with closing quotation mark

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevOpsProject.dll","--environment=Development"]
