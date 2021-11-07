#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CICD Git/CICD Git.csproj", "CICD Git/"]
RUN dotnet restore "CICD Git/CICD Git.csproj"
COPY . .
WORKDIR "/src/CICD Git"
RUN dotnet build "CICD Git.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CICD Git.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CICD Git.dll"]