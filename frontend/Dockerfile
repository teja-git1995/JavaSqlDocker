FROM node:18-alpine as build

WORKDIR /app

COPY package.json ./

# Install dependencies including a compatible ajv
RUN npm install --legacy-peer-deps && npm install ajv@^6.12.6

COPY . .

RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

