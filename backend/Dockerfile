# Etapa de build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copiar o arquivo de solução e o projeto para restaurar as dependências
COPY backend.sln .
COPY teste.csproj ./teste/

# Restaurar as dependências do projeto específico
WORKDIR /app/teste
RUN dotnet restore

# Copiar o restante do código
COPY . .

# Realizar a publicação do projeto específico
RUN dotnet publish teste.csproj -c Release -o /app/publish

# Etapa de execução
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Copiar os artefatos da etapa de build
COPY --from=build /app/publish .

# Expor a porta correta, que é 8080
EXPOSE 8080

# Executar o aplicativo
ENTRYPOINT ["dotnet", "teste.dll"]
