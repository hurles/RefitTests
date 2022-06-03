FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RefitTestApi/RefitTestApi.csproj", "RefitTestApi/"]
RUN dotnet restore "RefitTestApi/RefitTestApi.csproj"
COPY . .
WORKDIR "/src/RefitTestApi"
RUN dotnet build "RefitTestApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RefitTestApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RefitTestApi.dll"]
