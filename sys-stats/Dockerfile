FROM node:lts
EXPOSE 3000
COPY ./ ./
RUN npm install
RUN npm run build
CMD ["npm", "start"]