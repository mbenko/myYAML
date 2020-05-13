#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["myNewDadApp/myNewDadApp.csproj", "myNewDadApp/"]
RUN dotnet restore "myNewDadApp/myNewDadApp.csproj"
COPY . .
WORKDIR "/src/myNewDadApp"
RUN dotnet build "myNewDadApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "myNewDadApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myNewDadApp.dll"]