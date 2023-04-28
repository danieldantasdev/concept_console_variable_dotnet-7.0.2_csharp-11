FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["variables_dotnet-7/variables_dotnet-7.csproj", "variables_dotnet-7/"]
RUN dotnet restore "variables_dotnet-7/variables_dotnet-7.csproj"
COPY . .
WORKDIR "/src/variables_dotnet-7"
RUN dotnet build "variables_dotnet-7.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "variables_dotnet-7.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "variables_dotnet-7.dll"]
