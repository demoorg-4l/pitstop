FROM mcr.microsoft.com/dotnet/sdk:8.0 AS stage

WORKDIR /app 

COPY *.csproj .

RUN dotnet restore

COPY . .

RUN donet publish -c Release -o out


FROM mcr.microsoft.com/donet/sdk:8.0

WORKDIR /app 

COPY --from=stage /app/out .

EXPOSE 5000

ENV ASPNETCORE_URLS http://*:5000

ENTRYPOINT [ "donet" , "Pitstop.VehicleManagementAPI.dll" ]