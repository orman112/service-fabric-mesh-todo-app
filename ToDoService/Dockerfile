FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 20003

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ToDoService/ToDoService.csproj ToDoService/
RUN dotnet restore ToDoService/ToDoService.csproj
COPY . .
WORKDIR /src/ToDoService
RUN dotnet build ToDoService.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ToDoService.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ToDoService.dll"]