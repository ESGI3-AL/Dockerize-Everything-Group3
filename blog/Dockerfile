#Créer un Dockerfile pour cette application en mode production
FROM rustlang/rust:nightly

RUN apt-get update && apt-get install -y libpq-dev build-essential

ENV PATH="/root/.cargo/bin:${PATH}"

 WORKDIR /app

 COPY . .

RUN cargo install diesel_cli --no-default-features --features postgres

 

RUN cargo build --release

CMD diesel migration run &&./target/release/blog

