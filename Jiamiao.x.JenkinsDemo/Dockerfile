#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["./Jiamiao.x.JenkinsDemo/Jiamiao.x.JenkinsDemo.csproj", "Jiamiao.x.JenkinsDemo/"]
RUN dotnet restore "Jiamiao.x.JenkinsDemo/Jiamiao.x.JenkinsDemo.csproj"
COPY . .
WORKDIR "/src/Jiamiao.x.JenkinsDemo"
RUN dotnet build "Jiamiao.x.JenkinsDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Jiamiao.x.JenkinsDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Jiamiao.x.JenkinsDemo.dll"]