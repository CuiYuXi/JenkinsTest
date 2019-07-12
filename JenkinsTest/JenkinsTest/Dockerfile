FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["JenkinsTest.csproj", "JenkinsTest/"]
RUN dotnet restore "JenkinsTest/JenkinsTest.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "JenkinsTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "JenkinsTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "JenkinsTest.dll"]