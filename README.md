# Kubernetes Learning Documentation

Welcome to my **Kubernetes Learning Documentation**! This repository is a structured knowledge base documenting my journey learning Kubernetes, organized with **MkDocs** and hosted on **GitHub Pages**.

## 📖 Overview

This project contains notes, tutorials, examples, and best practices covering core Kubernetes concepts, including:

* **Pods** – the smallest deployable units in Kubernetes
* **Deployments** – managing application lifecycles
* **Services** – exposing applications inside and outside the cluster
* **ConfigMaps & Secrets** – managing configuration and sensitive data
* **Namespaces** – organizing cluster resources
* **Volumes & Persistent Storage** – managing data in Kubernetes

…and more. The content is designed to help both beginners and intermediate learners understand Kubernetes step by step.

## 🛠️ Tools Used

* **[MkDocs](https://www.mkdocs.org/)** – for creating the documentation site
* **[MkDocs Material](https://squidfunk.github.io/mkdocs-material/)** – optional theme for a modern look
* **GitHub Pages** – hosting the documentation online

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Rahul-404/kubernetes-learning.git
cd kubernetes-learning
```

### 2. Install MkDocs

```bash
pip install mkdocs
```

### 3. Serve locally

```bash
mkdocs serve
```

Visit `http://127.0.0.1:8000/` to preview the site.

### 4. Deploy to GitHub Pages

```bash
mkdocs gh-deploy
```

Your site will be live at:
`https://rahul-404.github.io/kubernetes-learning/`

## 🗂️ Structure

```
kubernetes-learning/
│
├── docs/
│   ├── index.md        # Home page
│   ├── intro.md        # Introduction to Kubernetes
│   ├── pods.md         # Pods
│   ├── deployments.md  # Deployments
│   └── ...             # Other topics
│
├── mkdocs.yml           # Site configuration
└── README.md            # This file
```

## 🌟 Contributing

Feel free to submit **issues** or **pull requests** if you have suggestions, corrections, or additional learning notes to contribute.

## 📄 License

This repository is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---
