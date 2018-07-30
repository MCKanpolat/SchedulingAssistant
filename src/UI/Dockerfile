FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 59174
EXPOSE 44343

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY UI/UI.csproj UI/
RUN dotnet restore UI/UI.csproj
COPY . .
WORKDIR /src/UI
RUN dotnet build UI.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish UI.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "UI.dll"]
