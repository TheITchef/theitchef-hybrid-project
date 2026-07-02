📌 Project Overview

This homelab mirrors real corporate hybrid identity and infrastructure design.
It includes:

    Active Directory Domain Services

    Two‑tier PKI

    ADFS + WAP federation

    Azure AD Connect

    Hyper‑V + ESXi compute

    Cisco L3 routing + VLAN segmentation

    Terraform + PowerShell automation

    Full documentation set

    Professional project governance

The goal is to provide a realistic, interview‑ready, enterprise‑grade environment.
📁 Repository Structure
Documentation

    project-governance — charter, scope, risks, baseline

    architecture — identity, PKI, network, compute, Azure

    design — VLAN plan, VM placement, trust boundaries

    procedures — deployment guides

    diagrams — logical + physical diagrams

Automation

    powershell — AD, PKI, Hyper‑V, ESXi scripts

    terraform — modules, environments, state

    scripts — Windows + Linux utilities

Configuration

    cisco — WS‑3850, C3560CG, 891F configs

    hyperv

    esxi

    pki

    ad

    azure

Assets

    inventory — hardware + network inventory

    exports — exported configs

    scratchpad — temporary notes

Threads

Topic‑based discussion folders for Obsidian or Git:

    01-core

    02-infrastructure

    03-design

    04-support

    05-learning

🎯 Goals

    Build a complete hybrid identity environment

    Learn enterprise‑grade PKI, ADFS, and Azure AD Connect

    Practice Cisco L3 routing and VLAN segmentation

    Deploy Hyper‑V and ESXi compute layers

    Automate with PowerShell and Terraform

    Maintain professional documentation and project governance

    Create an interview‑ready architecture portfolio

🧱 Architecture Components

    Identity: AD DS, DNS, DHCP, Azure AD Connect

    PKI: Linux Root CA, Windows Issuing CA

    Federation: ADFS + WAP

    Compute: Hyper‑V host + ESXi cluster

    Network: Cisco WS‑3850, C3560CG, 891F

    Automation: PowerShell + Terraform

    Documentation: Full enterprise‑grade set

⚙️ How to Use This Repository

    Start with project-governance

    Review system-architecture-overview

    Follow the design documents (VLAN plan, VM placement)

    Apply configurations from the config/ directory

    Use automation from src/

    Maintain documentation as the environment evolves

📜 License

This homelab project is for personal learning, professional development, and architectural practice.# theitchef hybrid homelab
