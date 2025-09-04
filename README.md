# Docker-n8n
n8n Docker Compose
# Docker & Docker Compose auf Ubuntu

Alles in einem Block: Installation, Docker Compose, Container starten und Netzwerkzugriff.

# 1. System aktualisieren
sudo apt update && sudo apt upgrade -y
sudo apt install -y ca-certificates curl gnupg lsb-release

# 2. Docker GPG-Key hinzufügen
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 3. Docker-Repository einbinden
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 4. Docker Engine & Compose installieren
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 5. Docker testen
sudo docker run hello-world

# 6. Optional: Docker ohne sudo nutzen
sudo usermod -aG docker $USER
newgrp docker

# 7. Beispiel: Nginx Container mit Docker Compose starten
cat > docker-compose.yml <<EOL
version: "3.9"
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    restart: unless-stopped
EOL

docker compose up -d
docker compose ps

# 8. Zugriff im Netzwerk
# Browser: http://<SERVER-IP>:8080
