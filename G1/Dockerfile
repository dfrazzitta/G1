#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["G1/G1.csproj", "G1/"]
RUN dotnet restore "G1/G1.csproj"
COPY . .
WORKDIR "/src/G1"
RUN dotnet build "G1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "G1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "G1.dll"]