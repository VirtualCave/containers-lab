FROM golang AS builder

COPY * /app/

WORKDIR /app

RUN go build

FROM golang

COPY --from=builder /app ./

ENTRYPOINT [ "./homer-golang" ]