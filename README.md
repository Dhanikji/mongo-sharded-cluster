📌 MongoDB Sharded Cluster + Replication + Indexing + Monitoring (Prometheus + Grafana)
This project demonstrates a production-grade MongoDB Cluster using:
✅ 3 Shards (each a replica set)
✅ Config Servers
✅ Mongos Router
✅ Authentication (SCRAM-SHA-256)
✅ Keyfile (internal cluster auth)
✅ Indexing (Regular, Unique, Compound, Hashed)
✅ Monitoring with Prometheus + Grafana
✅ Docker & Docker-Compose setup
✅ Real cluster behavior: shard balancing, chunk splits, failover, metrics
This project is fully deployed using Docker Compose, making it easy to run on any system.

🧱 Architecture Overview
                   ┌────────────────────┐
                   │      Client         │
                   └─────────┬──────────┘
                             │
                     (mongos router)
                             │
       ┌───────────────────────────────────────────────┐
       │                                               │
┌────────────┐   ┌────────────┐   ┌────────────┐
│ Shard1 RS  │   │ Shard2 RS  │   │ Shard3 RS  │
└────────────┘   └────────────┘   └────────────┘
       │               │               │
       └───────── Config Servers RS ───┘


🚀 How to Run
1️⃣ Clone the Repository
git clone https://github.com/Dhanikji/mongo-sharded-cluster
cd mongo-sharded-cluster

2️⃣ Start the Cluster
docker-compose up -d

3️⃣ View Containers
docker ps


🔐 Authentication & Keyfile
MongoDB Cluster uses:


SCRAM-SHA-256 for user authentication


Keyfile for internal node-to-node authentication


Keyfile ensures only valid replica set members can join the cluster.

📚 Indexing Used in This Project
This project covers four important index types:
1️⃣ Regular Index
db.users.createIndex({ username: 1 })

Speeds up equality & sorting queries
Faster search by username

2️⃣ Unique Index
db.users.createIndex({ email: 1 }, { unique: true })

Guarantees no duplicate emails
Used for login or identity fields
Prevents inserting same email twice

3️⃣ Compound Index
db.users.createIndex({ country: 1, age: -1 })

Optimized for queries like:
db.users.find({ country: "India" }).sort({ age: -1 })


4️⃣ Hashed Index (for Sharding)
sh.shardCollection("trainingDB.hashCol", { userId: "hashed" })

Helps distribute documents evenly across shards.

🧪 Monitoring Setup (Prometheus + Grafana)
Prometheus:
Runs at:
http://localhost:9090

Example queries:
QueryMeaningmongodb_upMongoDB Exporter running or notmongodb_connectionsCurrent DB connectionsmongodb_op_counters_totalRead/write operations
Grafana:
Runs at:
http://localhost:3000

Default login:
username: admin
password: admin

Dashboards included:


MongoDB General Dashboard


MongoDB Exporter Dashboard


Cluster Health Panels



⚙️ Important Commands Used
View cluster status:
sh.status()

View replication:
rs.status()

Index performance:
db.users.find({...}).explain("executionStats")

Show all indexes:
db.users.getIndexes()

Show connections:
db.serverStatus().connections


## 📸 Screenshots

### 1️⃣ Grafana Dashboard
![Grafana Dashboard](docs/grafana.png)

---

### 2️⃣ Prometheus Metrics
![Prometheus Metrics](docs/prometheus.png)

---

### 3️⃣ MongoDB Sharded Cluster Running (Docker Containers)
![Cluster Running](docs/cluster.png)

