FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["BlazorInAspMvc/BlazorInAspMvc.csproj", "BlazorInAspMvc/"]
RUN dotnet restore "BlazorInAspMvc/BlazorInAspMvc.csproj"
COPY . .
WORKDIR "/src/BlazorInAspMvc"
RUN dotnet build "BlazorInAspMvc.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorInAspMvc.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorInAspMvc.dll"]
