FROM openfaas/classic-watchdog:0.13.4 as watchdog

FROM alpine:3.9

RUN apk add git curl nodejs npm

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

RUN git clone https://github.com/RoryH/dublinbus-luas-api 
RUN cd dublinbus-luas-api
RUN npm install
RUN npm start &

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV fprocess="xargs curl -s"
# Set to true to see request in function logs

EXPOSE 8080
HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

CMD ["fwatchdog"]
