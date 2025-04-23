# Deploy Go Apps on Google Cloud Serverless Platforms

---

## Overview

Go is an open source programming language by Google designed to build fast, reliable, and efficient software. In this lab, you'll deploy a simple Go app across three serverless platforms: Cloud Run, Cloud Functions, and App Engine. You'll also interact with Firestore and BigQuery using the app.

---

## Objectives

- Set up a Firestore database and import data
- Explore data in BigQuery and Firestore
- Deploy a Go app to:
  - Cloud Run
  - Cloud Functions
  - App Engine
- Examine and test the Go app on each platform

---

## What is Go?

Go (golang) is a compiled, strongly typed language ideal for cloud applications due to its efficiency and support for concurrency. Go applications are built from packages and are typically faster than interpreted languages like Python or JavaScript.

---

## Serverless Platforms

Serverless computing abstracts infrastructure, enabling:
- No server management
- Auto-scaling
- Pay-per-use
- Stateless HTTP apps

### Platforms used in this lab:
- **Cloud Run**
- **Cloud Functions**
- **App Engine**

---

## Cloud Build

Cloud Build executes builds on GCP infrastructure. It supports Docker containers and can build from GitHub or Cloud Storage sources.

---

## Google Cloud Data Drive App

The `gcp-data-drive` Go app exposes data via HTTP URL patterns from Firestore and BigQuery:

- **Firestore**: `/fs/[PROJECT_ID]/[COLLECTION]/[DOCUMENT]`
- **BigQuery**: `/bq/[PROJECT_ID]/[DATASET]/[TABLE]`

---

## Deployment Commands
Running the Samar.sh file should **Deploy Go Apps on Google Cloud Serverless Platforms** and complete all tasks at once.

### Set up environment

```bash
export REGION=
export PROJECT_ID=$(gcloud info --format="value(config.project)")
git clone https://github.com/GoogleCloudPlatform/DIY-Tools.git
gcloud firestore import gs://$PROJECT_ID-firestore/prd-back
```
---

### Configure IAM and build permissions

```bash
PROJECT_NUMBER=$(gcloud projects list --filter="PROJECT_ID=$PROJECT_ID" --format="value(PROJECT_NUMBER)")
SERVICE_ACCOUNT_EMAIL="${PROJECT_NUMBER}@cloudbuild.gserviceaccount.com"
gcloud projects add-iam-policy-binding ${PROJECT_ID} \
    --member "serviceAccount:${SERVICE_ACCOUNT_EMAIL}" \
    --role "roles/artifactregistry.reader"
```
---
