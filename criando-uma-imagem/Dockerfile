FROM php:7.2-cli

ENV GREETING "Mundo"

COPY ./ /code

RUN php -m

WORKDIR /code

VOLUME [ "/code" ]

EXPOSE 80

ENTRYPOINT [ "php", "-S", "0.0.0.0:80", "-t" ]

CMD [ "/code" ]