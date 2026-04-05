# 🚀 K8s Cluster Automation using AWX & Ansible

This project automates the deployment of a Kubernetes (K8s) cluster using **AWX (Ansible Tower)** and Ansible Galaxy roles.

It provides a simple and reusable way to install Kubernetes across multiple nodes using centralized automation.

---

## 📌 Overview

This project uses **Ansible playbooks executed via AWX** to install and configure a Kubernetes cluster.

Instead of writing custom roles, it leverages:

* External role: `TalhaJuikar.kubernetes`
* Ansible collection: `community.general`

The automation is designed to be:

* Simple
* Repeatable
* Easy to integrate with AWX

---

## 📂 Project Structure

```bash
k8s-cluster-automation/
│── collections/
│   └── requirements.yml      # Ansible collections (community.general)
│
│── playbooks/
│   └── site.yml              # Main playbook to install Kubernetes
│
│── requirements.yml          # Ansible Galaxy role (TalhaJuikar.kubernetes)
│
│── README.md
```

---

## ⚙️ How It Works

The main playbook:

```yaml
- name: Install kubernetes
  hosts: all
  become: true
  roles:
    - TalhaJuikar.kubernetes
```

### Execution Flow:

1. AWX runs the playbook on all target nodes
2. The role `TalhaJuikar.kubernetes`:

   * Installs Kubernetes components
   * Configures control plane and worker nodes
3. `community.general` collection provides additional modules if needed

---

## 🛠️ Tech Stack

* Ansible
* AWX (Ansible Tower)
* Kubernetes (K8s)
* Ansible Galaxy Roles
* Ansible Collections

---

## 🚀 Setup

### 1. Install Required Role

```bash
ansible-galaxy install -r requirements.yml
```

---

### 2. Install Required Collection

```bash
ansible-galaxy collection install -r collections/requirements.yml
```

---

## ▶️ Running the Project

### Using AWX (Recommended)

1. Create a **Project** in AWX and link this repository
2. Create an **Inventory** (add your nodes)
3. Add **Credentials** (SSH access)
4. Create a **Job Template**:

   * Playbook: `playbooks/site.yml`
5. Launch the job 🚀

---

## ✔️ Verification

After execution:

```bash
kubectl get nodes
kubectl get pods -a
```

All nodes should be in **Ready** state.

---

## 📊 Benefits

* 🔁 Repeatable Kubernetes deployment
* ⚡ Fast cluster setup using automation
* 🧩 Reuse of tested Galaxy roles
* 🖥️ Centralized execution via AWX
