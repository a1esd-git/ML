# Берем официальный образ Python (slim версия, чтобы не весил 2 ГБ)
FROM python:3.11-slim

# Устанавливаем системные зависимости
# libgomp1 критически важен для работы LightGBM и XGBoost
RUN apt-get update && apt-get install -y \
    build-essential \
    libgomp1 \
    && rm -rf /var/lib/apt/lists/*

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем список библиотек и устанавливаем их
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Копируем все файлы проекта в контейнер
COPY . .

# Открываем порт для Jupyter
EXPOSE 8888

# Команда по умолчанию (будет переопределена в docker-compose для удобства)
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--ServerApp.token=", "--ServerApp.password="]