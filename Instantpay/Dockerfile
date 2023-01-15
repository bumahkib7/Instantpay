FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Instantpay/Instantpay.csproj", "Instantpay/"]
RUN dotnet restore "Instantpay/Instantpay.csproj"
COPY . .
WORKDIR "/src/Instantpay"
RUN dotnet build "Instantpay.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Instantpay.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Instantpay.dll"]
