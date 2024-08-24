FROM mcr.microsoft.com/dotnet/sdk:8.0 AS stage

WORKDIR /app 

COPY *.csproj .

RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o out /app/csproj


FROM mcr.microsoft.com/dotnet/sdk:8.0

WORKDIR /app 

COPY --from=stage /app/out .

EXPOSE 5000

ENV ASPNETCORE_URLS http://*:5000

HEALTHCHECK --interval=30s --timeout=3s --retries=1 CMD curl --silent --fail http://localhost:5000/hc || exit 1


ENTRYPOINT [ "donet" , "Pitstop.VehicleManagementAPI.dll" ]