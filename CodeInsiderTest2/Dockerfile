FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CodeInsiderTest2/CodeInsiderTest2.csproj", "CodeInsiderTest2/"]
RUN dotnet restore "CodeInsiderTest2/CodeInsiderTest2.csproj"
COPY . .
WORKDIR "/src/CodeInsiderTest2"
RUN dotnet build "CodeInsiderTest2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CodeInsiderTest2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CodeInsiderTest2.dll"]
