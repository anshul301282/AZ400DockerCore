#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AZ400DockerCore5/AZ400DockerCore5.csproj", "AZ400DockerCore5/"]
RUN dotnet restore "AZ400DockerCore5/AZ400DockerCore5.csproj"
COPY . .
WORKDIR "/src/AZ400DockerCore5"
RUN dotnet build "AZ400DockerCore5.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AZ400DockerCore5.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AZ400DockerCore5.dll"]