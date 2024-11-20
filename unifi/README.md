# UniFi Network Controller

Make data directories

```bash
mkdir -p ./data/db
mkdir -p ./data/network-application
```

Run it

```bash
docker compose up -f network-controller.yaml -d 
```

Unifi app will be available on `https://<host-ip>:8443`
