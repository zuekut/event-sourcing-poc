FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["EventSourcingPoc/EventSourcingPoc.csproj", "EventSourcingPoc/"]
RUN dotnet restore "EventSourcingPoc/EventSourcingPoc.csproj"
COPY . .
WORKDIR "/src/EventSourcingPoc"
RUN dotnet build "EventSourcingPoc.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "EventSourcingPoc.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EventSourcingPoc.dll"]