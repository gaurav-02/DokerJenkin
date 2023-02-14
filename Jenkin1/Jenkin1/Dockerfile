#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Jenkin1/Jenkin1.csproj", "Jenkin1/"]
RUN dotnet restore "Jenkin1/Jenkin1.csproj"
COPY . .
WORKDIR "/src/Jenkin1"
RUN dotnet build "Jenkin1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Jenkin1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Jenkin1.dll"]