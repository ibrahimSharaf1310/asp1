
# المرحلة الأولى: البناء
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# نسخ كل ملفات المشروع
COPY . ./

# استرجاع الحزم وبناء المشروع
RUN dotnet restore
RUN dotnet publish -c Release -o out

# المرحلة الثانية: التشغيل
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# نسخ الملفات المنشورة من مرحلة البناء
COPY --from=build /app/out ./

# ضبط التطبيق للاستماع على البورت 10000 حسب ما يحتاجه Render
ENV ASPNETCORE_URLS=http://0.0.0.0:10000
EXPOSE 10000

# تشغيل التطبيق
ENTRYPOINT ["dotnet", "test.dll"]
