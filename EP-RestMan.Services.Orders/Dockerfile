FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY EP-RestMan.Services.Orders/EP-RestMan.Services.Orders.csproj EP-RestMan.Services.Orders/
RUN dotnet restore EP-RestMan.Services.Orders/EP-RestMan.Services.Orders.csproj
COPY . .
WORKDIR /src/EP-RestMan.Services.Orders
RUN dotnet build EP-RestMan.Services.Orders.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish EP-RestMan.Services.Orders.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EP-RestMan.Services.Orders.dll"]
