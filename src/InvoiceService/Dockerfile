FROM mcr.microsoft.com/dotnet/sdk:8.0 AS stage 

WORKDIR /app 

COPY *.csproj .

RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/sdk:8.0

WORKDIR /app

COPY --from=stage /app/out .

ENTRYPOINT ["dotnet", "Pitstop.InvoiceService.dll"]