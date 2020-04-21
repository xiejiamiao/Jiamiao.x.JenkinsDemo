# 指定运行是镜像
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app

# 指定编译和发布镜像
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
# 设置工作目录为src
WORKDIR /src
# 拷贝所有文件到容器中的工作目录
COPY . ./
RUN dotnet restore "./Jiamiao.x.JenkinsDemo.csproj" && dotnet build "./Jiamiao.x.JenkinsDemo.csproj" -c Release -o /app/build && dotnet publish "./Jiamiao.x.JenkinsDemo.csproj" -c Release -o /app/publish

FROM base as final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT [ "dotnet","Jiamiao.x.JenkinsDemo.dll" ]