version: '3'
services:
  loki:
    image: grafana/loki:latest
    ports:
      - "3100:3100"
    command: -config.file=/etc/loki/local-config.yaml
    volumes:
      - ./loki-config:/etc/loki

  promtail:
    image: grafana/promtail:latest
    volumes:
      - ./promtail-config:/etc/promtail
    command: -config.file=/etc/promtail/promtail-config.yml

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=your_password
    volumes:
      - ./grafana-data:/var/lib/grafana
    depends_on:
      - loki

  nodejs-app:
    build:
      context: ./nodejs-app
    ports:
      - "8080:8080"
    logging:
      driver: "loki"
      options:
        loki-url: "http://loki:3100/loki/api/v1/push"
        loki-retries: "5"
        loki-batch-size: "400"
        loki-batch-wait: "1s"

volumes:
  grafana-data:

Explanation: 

loki: The Loki service for log aggregation. It uses a local configuration file provided in the ./loki-config directory.

promtail: The Promtail service for log collection. It uses a configuration file provided in the ./promtail-config directory.

grafana: The Grafana service for visualization. It uses environment variables to set up an admin password and uses a volume to persist data.

nodejs-app: Your Node.js application. It's built from a Dockerfile in the ./nodejs-app directory. The application's logs are sent to Loki for aggregation and visualization.

Make sure to replace your_password in the Grafana section with a secure password for the Grafana admin user. Additionally, you need to set up the necessary Loki and Promtail configurations in the ./loki-config and ./promtail-config directories, respectively. These configurations should match your specific log collection requirements and log formats.

To start the service
docker-compose up

This will start all the defined services and set up log collection and visualization for your Node.js application using Loki, Grafana, and Promtail.
