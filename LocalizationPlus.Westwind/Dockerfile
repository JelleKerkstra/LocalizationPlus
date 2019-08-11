FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["LocalizationPlus.Westwind/LocalizationPlus.Westwind.csproj", "LocalizationPlus.Westwind/"]
RUN dotnet restore "LocalizationPlus.Westwind/LocalizationPlus.Westwind.csproj"
COPY . .
WORKDIR "/src/LocalizationPlus.Westwind"
RUN dotnet build "LocalizationPlus.Westwind.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "LocalizationPlus.Westwind.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LocalizationPlus.Westwind.dll"]