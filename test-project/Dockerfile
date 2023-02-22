FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["test-project.csproj", "./"]
RUN dotnet restore "test-project.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "test-project.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "test-project.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "test-project.dll"]
