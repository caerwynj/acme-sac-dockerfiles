FROM arm32v7/alpine:3.16

RUN apk add build-base libx11-dev libxext-dev linux-headers -t build
#RUN apk add libx11 libxext

RUN addgroup -S inferno
RUN adduser --disabled-password --ingroup inferno inferno
USER inferno

ENV INFERNO=/usr/acme-sac
ENV objtype=arm
WORKDIR $INFERNO

COPY --chown=inferno . $INFERNO

ENV PATH="$INFERNO/sys/Linux/${objtype}/bin:${PATH}"
RUN cd sys \
	&&  ./makemk.sh \
	&& mk clean \
	&& mk install \
	&& mk clean

EXPOSE 8080
ENTRYPOINT ["emu"]
CMD ["-r", "/usr/acme-sac"]
