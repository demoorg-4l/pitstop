FROM mcr.microsoft.com/dotnet/sdk:8.0 AS stage

WORKDIR /app 

ENV NODE_VERSION=20.17.0

RUN apt-get -y update \
    && apt-get install -y curl \
    && curl -sL https://deb.nodesource.com/setup_${NODE_VERSION} | sh - \ 
    && apt-get install -y nodejs 

RUN npm install --global gulp-cli

COPY *.csproj ./

RUN dotnet restore

COPY . .

RUN npm install

RUN gulp default


RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app 

COPY --from=stage /app/out .

EXPOSE 7005

ENV ASPNETCORE_URLS http://*:7005

ENTRYPOINT ["dotnet", "Pitstop.WebApp.dll"]