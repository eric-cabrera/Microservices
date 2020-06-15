#we're creating a a core application vertion 3.1
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
#than we'l be swiching to the app directory 
WORKDIR /app
# and we will expose it in port 80 443
EXPOSE 80
EXPOSE 443


#we used the section for building the app
#we be using only the files to compile the app 
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["HelloAspNetCore.csproj", "./"] #copy project file into the root ./
RUN dotnet restore "./HelloAspNetCore.csproj"  #restored all dependencies 
#copy all file  here
COPY . . 
#WORKDIR "/src/."  remove this line is not needede
RUN dotnet build "HelloAspNetCore.csproj" -c Release -o /app/build


#then we publish 
FROM build AS publish
RUN dotnet publish "HelloAspNetCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloAspNetCore.dll"]
