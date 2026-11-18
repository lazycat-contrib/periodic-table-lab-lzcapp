FROM node:22-alpine AS build
WORKDIR /app
ADD source.tar.gz .
RUN sh -c 'cd brin666-periodic-table-lab-* && mv * .[!.]* .. 2>/dev/null; cd .. && rmdir brin666-periodic-table-lab-*'
RUN npm ci
RUN npm run build

FROM nginx:1.27-alpine AS runtime
RUN adduser -D -H -u 1000 webuser
RUN sed -i 's/user  nginx;/user  webuser;/' /etc/nginx/nginx.conf \
    && sed -i 's/listen  80;/listen  8080;/' /etc/nginx/nginx.conf \
    && sed -i 's/listen  \[::\]:80;/listen  [::]:8080;/' /etc/nginx/nginx.conf \
    && chmod -R g+rwx /var/cache/nginx /var/run \
    && chown -R 1000:1000 /var/cache/nginx /var/run
COPY --from=build /app/dist /usr/share/nginx/html
ENV TZ=Asia/Shanghai
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD wget -q -O /dev/null http://127.0.0.1:8080/ || exit 1
CMD ["nginx", "-g", "daemon off;"]
