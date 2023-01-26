FROM microsoft/dotnet:6.0-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 56053
EXPOSE 44301

FROM microsoft/dotnet:6.0-sdk AS build
WORKDIR /src
COPY ["Derdeyn.GraduaatIconizer.Web/Derdeyn.GraduaatIconizer.Web.csproj", "Derdeyn.GraduaatIconizer.Web/"]
RUN dotnet restore "Derdeyn.GraduaatIconizer.Web/Derdeyn.GraduaatIconizer.Web.csproj"
COPY . .
WORKDIR "/src/Derdeyn.GraduaatIconizer.Web"
RUN dotnet build "Derdeyn.GraduaatIconizer.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Derdeyn.GraduaatIconizer.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Derdeyn.GraduaatIconizer.Web.dll"]