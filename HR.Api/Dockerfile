FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["HR.Api/HR.Api.csproj", "HR.Api/"]
RUN dotnet restore "HR.Api/HR.Api.csproj"
COPY . .
WORKDIR "/src/HR.Api"
RUN dotnet build "HR.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HR.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HR.Api.dll"]
