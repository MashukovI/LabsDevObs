# Используем базовый образ с ASP.NET 8.0
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base

# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

# Используем SDK
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Копируем файлы в контейнер
COPY . /src

# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /src

# Устанавливаем зависимости приложения и параметры компиляции
RUN ls
RUN dotnet restore
RUN dotnet build "./LabsDevObs.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "./LabsDevObs.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish ./

# Определяем команду запуска контейнера
ENTRYPOINT ["dotnet", "LabsDevObs.dll"]
