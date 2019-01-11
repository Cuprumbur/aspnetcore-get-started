#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1803 AS base
WORKDIR /app
EXPOSE 40028
EXPOSE 44303

FROM microsoft/dotnet:2.1-sdk-nanoserver-1803 AS build
WORKDIR /src
COPY ["EFGetStarted.AspNetCore.NewDb/EFGetStarted.AspNetCore.NewDb.csproj", "EFGetStarted.AspNetCore.NewDb/"]
RUN dotnet restore "EFGetStarted.AspNetCore.NewDb/EFGetStarted.AspNetCore.NewDb.csproj"
COPY . .
WORKDIR "/src/EFGetStarted.AspNetCore.NewDb"
RUN dotnet build "EFGetStarted.AspNetCore.NewDb.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "EFGetStarted.AspNetCore.NewDb.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EFGetStarted.AspNetCore.NewDb.dll"]