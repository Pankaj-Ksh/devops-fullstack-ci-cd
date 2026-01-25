# ---------- STAGE 1: Build ----------
FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# 👇 ADD THESE TWO LINES
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

RUN npm run build


# ---------- STAGE 2: Runtime ----------
FROM nginx:alpine

RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf

COPY --from=builder /app/dist /usr/share/nginx/html

RUN adduser -D appuser \
    && chown -R appuser:appuser /usr/share/nginx /var/cache/nginx /etc/nginx

USER appuser

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
