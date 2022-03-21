#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["FirstMVCProj/FirstMVCProj.csproj", "FirstMVCProj/"]
RUN dotnet restore "FirstMVCProj/FirstMVCProj.csproj"
COPY . .
WORKDIR "/src/FirstMVCProj"
RUN dotnet build "FirstMVCProj.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FirstMVCProj.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FirstMVCProj.dll"]