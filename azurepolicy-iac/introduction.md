---
hidden: true
---

# Introduction

This repo is both a tutorial and a fully deployable solution for automating the deployment of Azure Policies across a tenant using Azure DevOps.

At the core is a CI/CD-ready YAML pipeline (`azure-policy-pipeline`) that validates, tests, and deploys custom Azure Policy definitions and initiatives automatically when changes are committed. The solution includes reusable assignment templates scoped to a target management group, making it easy to scale governance across multiple subscriptions.

It also comes with:

* Prebuilt policy definitions (e.g., US region restrictions, AI/ML service denial)
* Security-focused initiatives (AKS Best Practices, CIS Foundations Benchmark v2.0.0-alpha)
* A structured folder layout and detailed README to guide implementation

Whether you're just getting started with policy-as-code or looking to standardize and scale compliance across your org, this repo will walk you through the _how_ and give you everything you need to deploy it immediately.
