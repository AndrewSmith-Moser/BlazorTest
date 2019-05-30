FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["BlazorServerSide.csproj", "BlazorServerSide/"]
RUN dotnet restore "BlazorServerSide/BlazorServerSide.csproj"
WORKDIR "/src/BlazorServerSide"
COPY . .
RUN dotnet build "BlazorServerSide.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BlazorServerSide.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BlazorServerSide.dll"]