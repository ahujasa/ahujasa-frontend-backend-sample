FROM node:lts
EXPOSE 3000
# EXPOSE 8000
COPY ./ ./
# RUN npm install http-proxy-middleware --save
RUN npm install
RUN npm run build
CMD ["npm", "start"]