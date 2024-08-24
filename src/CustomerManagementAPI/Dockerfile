FROM mcr.microsoft.com/dotnet/sdk:8.0 AS stage

WORKDIR /app 

COPY *.csproj .

RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o out 


FROM mcr.microsoft.com/dotnet/sdk:8.0

WORKDIR /app 

COPY --from=stage /app/out .

EXPOSE 5100

ENV ASPNETCORE_URLS http://*:5100


ENTRYPOINT [ "donet" , "Pitstop.CustomerManagementAPI.dll" ]