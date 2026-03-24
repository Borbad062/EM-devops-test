FROM python:3.13-alpine

RUN addgroup -g 1001 -S nonroot && \
    adduser -u 1001 -S nonroot -G nonroot -s /bin/sh

WORKDIR /usr/src/app

COPY app.py .

RUN chown -R nonroot:nonroot /usr/src/app
USER nonroot

EXPOSE 8080

CMD ["python", "app.py"]