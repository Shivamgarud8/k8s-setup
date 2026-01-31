#!/bin/bash
set -e

echo "======================================"
echo "   Kubernetes Cluster Setup Script"
echo "======================================"

# VARIABLES (change if needed)
REPO_URL="https://github.com/Shivamgarud8/k8s-setup.git"
REPO_DIR="k8s-setup"

# Clone repo if not exists
echo "📥 Cloning Kubernetes setup repository..."
if [ ! -d "$REPO_DIR" ]; then
    git clone $REPO_URL
else
    echo "Repo already exists, skipping clone."
fi

cd $REPO_DIR

# Set execute permissions on scripts
echo "🔐 Setting execute permission on scripts..."
chmod +x k8s-master.sh
chmod +x k8s-slave.sh

# Node selection
echo ""
echo "Select node type:"
echo "1️⃣  Master Node"
echo "2️⃣  Worker Node"
echo ""

read -p "Enter choice (1 or 2): " choice

if [ "$choice" == "1" ]; then
    echo "🚀 Running MASTER setup..."
    ./k8s-master.sh

elif [ "$choice" == "2" ]; then
    echo "🚀 Running WORKER setup..."
    ./k8s-slave.sh

    echo ""
    echo "🔑 Paste kubeadm join command from MASTER:"
    read -p "Join Command: " JOIN_CMD

    echo "⏳ Joining cluster..."
    sudo $JOIN_CMD --cri-socket unix:///run/containerd/containerd.sock

    echo "✅ Worker successfully joined the cluster!"

else
    echo "❌ Invalid choice. Please enter 1 or 2."
    exit 1
fi

echo "======================================"
echo " 🎉 Kubernetes Setup Completed"
echo "======================================"
