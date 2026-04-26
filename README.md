# Kafka Python Project

Small learning project following the Kafka crash course tutorial.

This project uses:

- Docker Desktop to run Kafka locally
- Python virtual environment for the app dependencies
- `confluent-kafka` for the Python producer and consumer

## Project Files

```text
docker-compose.yaml   # Starts the local Kafka container
producer.py           # Sends order events to Kafka
tracker.py            # Reads order events from Kafka
requirements.txt      # Python dependencies
README.md             # Project instructions
```

## 1. Install Docker Desktop

Download and install Docker Desktop:

```text
https://www.docker.com/products/docker-desktop/
```

After installing, open Docker Desktop and wait until it is running.

If Docker says WSL needs updating, open PowerShell as Administrator and run:

```powershell
wsl --update
wsl --shutdown
```

Then reopen Docker Desktop.

Check Docker from a new terminal:

```powershell
docker --version
docker compose version
```

## 2. Create and Activate Python Virtual Environment

From the project folder:

```powershell
cd C:\Neha\Project\Kafka_project
python -m venv .venv
.\.venv\Scripts\activate
```

When activated, the terminal should show `(.venv)`.

To leave the virtual environment:

```powershell
deactivate
```

## 3. Install Python Dependencies

With the virtual environment activated:

```powershell
pip install -r requirements.txt
```

If starting from scratch, install the dependency directly:

```powershell
pip install confluent-kafka
pip freeze > requirements.txt
```

## 4. Start Kafka Container

Make sure Docker Desktop is running.

From the project folder:

```powershell
docker compose up -d
```

Check that the Kafka container is running:

```powershell
docker ps
```

Stop the container:

```powershell
docker compose down
```

## 5. Run the Tracker

The tracker listens for messages from the `orders` topic.

Open one terminal:

```powershell
cd C:\Neha\Project\Kafka_project
.\.venv\Scripts\activate
python tracker.py
```

Keep this terminal open.

## 6. Run the Producer

Open a second terminal:

```powershell
cd C:\Neha\Project\Kafka_project
.\.venv\Scripts\activate
python producer.py
```

The producer sends one order event to Kafka. The tracker should receive and print it.

## Useful Kafka Commands

List topics:

```powershell
docker exec -it kafka kafka-topics --list --bootstrap-server localhost:9092
```

Describe the `orders` topic:

```powershell
docker exec -it kafka kafka-topics --bootstrap-server localhost:9092 --describe --topic orders
```

View all events in the `orders` topic:

```powershell
docker exec -it kafka kafka-console-consumer --bootstrap-server localhost:9092 --topic orders --from-beginning
```

## Debugging in VS Code

Select the virtual environment interpreter:

```text
Ctrl + Shift + P -> Python: Select Interpreter -> .venv\Scripts\python.exe
```

To debug:

1. Open `tracker.py` or `producer.py`.
2. Add a breakpoint on an executable line.
3. Press `F5`.
4. Choose `Python File` if VS Code asks.

For this project, start Kafka first, then run `tracker.py`, then run `producer.py`.
