#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.
# Comments added by Rafael San Vidal Hidalgo

# Download NET Core 5 Runtime
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

# Download NET Core 5 SDK  
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src

# Copy sources files and build the project
COPY ["Servicios.api.Libreria/Servicios.api.Libreria.csproj", "Servicios.api.Libreria/"]
RUN dotnet restore "Servicios.api.Libreria/Servicios.api.Libreria.csproj"
COPY . .
WORKDIR "/src/Servicios.api.Libreria"
RUN dotnet build "Servicios.api.Libreria.csproj" -c Release -o /app/build

# Publish product
FROM build AS publish
RUN dotnet publish "Servicios.api.Libreria.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Servicios.api.Libreria.dll"]