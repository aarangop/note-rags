# Notes RAG System

A complete event-driven RAG (Retrieval-Augmented Generation) system that
monitors your notes directory and enables AI-powered chat with your personal
knowledge base.

## Overview

This system automatically indexes your notes in a vector database by monitoring
file changes and processing them through a scalable cloud pipeline. Built with
Python file monitoring and AWS serverless architecture.

**Architecture:**

```
Local File Watcher (Python) → API Gateway → SQS Queue → Lambda Functions → Vector Database
                                    ↓
                               S3 Storage
```

## Components

### 📁 [File Watcher (`filewatcher/`)](./filewatcher/)

Python-based file monitoring service that:

- Watches your notes directory recursively
- Debounces file system events
- Sends changes to AWS API Gateway
- Supports multiple file formats (.md, .txt, .org)

### 🏗️ [Infrastructure (`infrastructure/`)](./infrastructure/)

Terraform modules for AWS infrastructure:

- **API Gateway**: Secure REST endpoint with API key authentication
- **SQS**: Message queue for decoupled event processing
- **S3**: Encrypted storage for note files and metadata
- **Lambda**: Functions for processing and vector database updates
- **IAM**: Least-privilege access controls

## Quick Start

### 1. Deploy Infrastructure

```bash
cd infrastructure/
cp terraform.tfvars.example terraform.tfvars
# Edit terraform.tfvars with your values
terraform init
terraform plan
terraform apply
```

### 2. Setup File Watcher

```bash
cd filewatcher/
cp .env.example .env
# Edit .env with your API Gateway URL and API key
uv sync
uv run notes-sync
```

### 3. Start Monitoring

Point the file watcher to your notes directory and it will automatically sync
changes to the cloud pipeline for processing.

## Key Features

- **🔄 Real-time Sync**: Instant detection and processing of file changes
- **🔐 Secure**: API key authentication and encrypted storage
- **📈 Scalable**: Event-driven architecture handles large note collections
- **🧠 AI-Ready**: Vector database integration for semantic search and RAG
- **🛠️ Modular**: Independent components that can be deployed separately

## Requirements

- **Python 3.11+** with [uv](https://docs.astral.sh/uv/) for file watcher
- **Terraform 1.0+** for infrastructure deployment
- **AWS Account** with appropriate permissions

## Development Status

- ✅ Python file watcher (complete)
- ✅ Terraform infrastructure modules (complete)
- ✅ API Gateway and SQS integration (complete)
- 🔄 Lambda processing functions (in progress)
- 📋 Vector database integration (planned)
- 📋 RAG chat interface (planned)

## License

MIT License - see individual component directories for details.
