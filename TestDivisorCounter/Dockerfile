FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["TestDivisorCounter/TestDivisorCounter.csproj", "TestDivisorCounter/"]
RUN dotnet restore "TestDivisorCounter/TestDivisorCounter.csproj"
COPY . .
WORKDIR "/src/TestDivisorCounter"
RUN dotnet build "TestDivisorCounter.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TestDivisorCounter.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "test", "TestDivisorCounter.dll"]
