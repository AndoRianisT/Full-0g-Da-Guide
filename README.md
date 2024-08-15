# 🚀 How to Set Up Your DA Client, DA Node, and DA Retriever

### Hey there! Ready to dive into setting up your own DA client, node, and retriever? We've got you covered! Here's a step-by-step guide with everything you need. Let's get started! 😎

---

## 🌟 DA Client Setup Guide 🌟

### 🛠 Hardware Requirements

To run your DA client smoothly, here’s what your system should have:

- **RAM**: 8 GB  
- **CPU**: 2 cores  
- **Bandwidth**: 100 MBps (Download/Upload)

### 🔧 Installation Steps

#### 1. Install Dependencies

**For Linux**:
```bash
sudo apt-get update
sudo apt-get install cmake
```

**For Mac**:
```bash
brew install cmake
```

#### 2. Install Go

**For Linux**:
- **Download** Go installer:
  ```bash
  wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
  ```
- **Extract** the archive:
  ```bash
  rm -rf /usr/local/go && tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
  ```
- **Add** Go to your PATH:
  ```bash
  export PATH=$PATH:/usr/local/go/bin
  ```

**For Mac**:
- **Download** the Go installer from [Go Download Page](https://go.dev/dl/go1.22.0.darwin-amd64.pkg). Open the package and follow the instructions.

#### 3. Download the DA Client Source Code

```bash
git clone -b v1.0.0-testnet https://github.com/0glabs/0g-da-client.git
```

### ⚙️ Configuration Time

Here’s a quick rundown of important configuration options:

| Field | Description |
| --- | --- |
| `--chain.rpc` | JSON RPC node endpoint for the blockchain |
| `--chain.private-key` | Your hex-encoded private key |
| `--combined-server.storage.kv-db-path` | Path to your leveldb storage |
| ... | *And many more! Adjust based on your setup.* |

### 🚀 Ready to Run!

To build the combined server:

```bash
make build
```

Then run it with your configuration:

```bash
./bin/combined \
  --chain.rpc L1_RPC_ENDPOINT \
  --chain.private-key YOUR_PRIVATE_KEY \
  --combined-server.log.level-file trace \
  --combined-server.log.level-std trace \
  --combined-server.log.path ./../run/run.log
```

You can tweak other parameters based on your system and needs!

---

## 🔐 DA Node Setup Guide

Now let's move on to setting up your very own DA Node! 🛠️

### 🛠️ Hardware Requirements

Here’s what you’ll need to keep things running smoothly:

- **Memory**: 16 GB  
- **CPU**: 8 cores  
- **Disk**: 1 TB NVME SSD  
- **Bandwidth**: 100 MBps (Download/Upload)

### 🔧 Installation

1. **Clone the Node Repository**:
    ```bash
    git clone https://github.com/0glabs/0g-da-node.git
    git checkout tags/v1.0.1 -b v1.0.1
    ```

2. **Build**:
    ```bash
    cargo build --release
    ./dev_support/download_params.sh
    ```

### ⚙️ Configuration

Create a `config.toml` file with fields like these:

```toml
log_level = "info"
data_path = "./db/"
encoder_params_dir = "params/"
grpc_listen_address = "0.0.0.0:34000"
eth_rpc_endpoint = "https://rpc-testnet.0g.ai"
socket_address = "<public_ip/dns>:34000"
```

**BLS Key Generation**:

If you don't have a BLS key, generate one:

```bash
cargo run --bin key-gen
```

Keep your BLS key safe! 🔐

### 🚀 Run the DA Node

```bash
./target/release/server --config cargo.toml
```

Your node will register itself, and you'll be ready to participate in the DA network! 🌐

---

## 📡 DA Retriever Setup Guide

Ready to retrieve some data? Let’s set up the DA Retriever next! 🕵️‍♂️

### 🛠️ Hardware Requirements

For the DA retriever, your setup should include:

- **RAM**: 8 GB  
- **CPU**: 2 cores  
- **Bandwidth**: 100 MBps (Download/Upload)

### 🔧 Installation

#### 1. Install Dependencies

**For Linux**:
```bash
sudo apt-get update
sudo apt-get install cmake build-essential protobuf-compiler
```

**For Mac**:
```bash
brew install cmake
```

#### 2. Install Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

#### 3. Clone the DA Retriever Source Code

```bash
git clone https://github.com/0glabs/0g-da-retriever.git
```

### ⚙️ Configuration

Configure your `run/config.toml`:

| Field | Description |
| --- | --- |
| `log_level` | Set log level |
| `grpc_listen_address` | Server listening address |
| `eth_rpc_endpoint` | JSON RPC node endpoint |

### 🚀 Run the Retriever

Once your configuration is all set:

```bash
cargo build --release
./target/release/retriever --config ./run/config.toml
```

And you're all set! 🎉 Your DA retriever is ready to pull data and help the network!

---

### 💡 And that's it!

You've now got everything you need to set up your DA client, node, and retriever. You're officially ready to dive deep into the world of data availability! 🌐
