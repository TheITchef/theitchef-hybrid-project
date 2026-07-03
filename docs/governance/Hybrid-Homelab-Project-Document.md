HYBRID HOMELAB PROJECT DOCUMENT

Version: 2026‑07‑01
Author: Ioannis Mintzivyris
Location: Upplands Väsby, Stockholm County, Sweden
1. Executive Summary

This project delivers a fully functional enterprise‑grade hybrid infrastructure environment combining on‑premises Active Directory, PKI, ADFS, Hyper‑V, ESXi, Cisco networking, and Azure AD integration.

The environment is designed to mirror real corporate architecture and provide transferable professional skills in identity, networking, compute, automation, and project management.

The project follows a structured PM methodology using Obsidian Kanban and Git feature‑branch workflows.
Every step is executed with overview → scope → expected outcome → documentation.
2. Project Purpose

Build a mini‑enterprise hybrid environment that supports:

    Identity and access management

    PKI and certificate lifecycle

    Federation and cloud integration

    Segmented Cisco networking

    Virtualization across Hyper‑V and ESXi

    Automation using PowerShell and Terraform

    Professional project management discipline

This environment is used for learning, certification preparation, interview readiness, and hands‑on engineering practice.
3. Project Scope
In Scope

    AD DS domain (theitchef.com)

    DNS, DHCP

    Azure AD Connect

    ADFS + WAP

    Two‑tier PKI

    Hyper‑V host (DL360G8)

    ESXi hosts (ESXi01, ESXi02)

    Cisco WS‑3850 (L3 core)

    Cisco C3560CG (OOB + access)

    Cisco 891F (WAN edge)

    Granular VLAN segmentation

    Routing, trunking, access port configuration

    Terraform automation

    PowerShell automation

    Git repo (single repo, multi‑branch)

    Obsidian Kanban board

    Documentation set

Out of Scope

    NSX, vCenter (future phases)

    Advanced GPO hardening

    Enterprise monitoring stack

    Multi‑site AD topology

    Production‑grade HA clusters

4. Requirements
Identity Requirements

    Deploy AD DS domain: theitchef.com

    Secondary DC for redundancy

    DNS + DHCP

    Azure AD Connect

    ADFS + WAP

    Secure UPN routing and name resolution

PKI Requirements

    Two‑tier PKI

    Offline Linux Root CA

    Online Windows Issuing CA

    Enterprise certificate templates

    PKI VLAN isolation

    Key protection

Networking Requirements

    Granular VLAN segmentation

    L3 routing on WS‑3850

    OOB network on C3560CG

    WAN edge on Cisco 891F

    Inter‑VLAN routing

    DHCP relay

    DNS reachability

    Zero assumptions about current configs

Compute Requirements

    Hyper‑V host

    ESXi cluster

    VM placement per VLAN

    vCenter readiness

Azure Requirements

    Azure AD Connect

    Hybrid identity

    Terraform automation

    Secure federation

Automation Requirements

    PowerShell automation

    Terraform IaC

    Git feature‑branch workflow

Project Management Requirements

    Obsidian Kanban

    Granular tasks

    Step‑by‑step execution

    Overview → scope → expected outcome → documentation

5. Architecture Overview
Identity Architecture

    T330 as primary DC

    Secondary DC VM

    DNS + DHCP

    Azure AD Connect

    ADFS + WAP

    UPN domain: theitchef.com

PKI Architecture

    Linux Root CA (offline)

    Windows Issuing CA (online)

    PKI VLAN isolation

    Enterprise templates

    Secure key storage

Network Architecture

    WS‑3850: L3 core routing

    C3560CG: OOB + access

    Cisco 891F: WAN edge

    Granular VLAN plan: Identity, PKI, ADFS, Hyper‑V host, Hyper‑V VMs, ESXi hosts, ESXi VMs, PAWs, OOB, Storage, WAN edge, Native VLAN

Compute Architecture

    Hyper‑V host

    ESXi01 + ESXi02

    VM networks aligned with VLAN plan

    Future vCenter support

Azure Architecture

    Azure AD Connect

    ADFS/WAP federation

    Terraform automation

    Hybrid identity

Automation Architecture

    Windows PAW → PowerShell, Git

    Linux PAW → Terraform, Root CA

    Git repo → feature‑branch workflow

    Obsidian Kanban → PM control

6. Deliverables
Technical Deliverables

    AD DS domain

    Secondary DC

    DNS + DHCP

    Azure AD Connect

    ADFS + WAP

    Two‑tier PKI

    Hyper‑V host + core VMs

    ESXi hosts segmented

    VLAN plan

    Routed network

    Terraform base structure

    PowerShell automation scripts

    Git repo

    Obsidian Kanban board

Documentation Deliverables

    Project Charter

    Current State

    VLAN Plan

    Network Topology

    Identity Architecture

    PKI Architecture

    Compute Layout

    Azure Integration

    Risk Assessment

    Mitigation Plan

7. Constraints

    Work must be done from Windows PAW

    No assumptions about device configuration

    Every step begins with an overview

    Granular documentation

    Single repo, multi‑branch

    VLAN plan must not be redesigned

    Enterprise‑grade alignment

    Hardware limitations

    Time constraints

8. Assumptions

    Hardware available

    Azure tenant accessible

    Domain owned

    Administrative access

    Structured guidance preferred

    Enterprise‑grade architecture desired

    No external dependencies beyond Azure

9. Risk Assessment
Technical Risks

    Misconfigured VLANs

    Routing loops

    PKI misconfiguration

    AD replication issues

    Hyper‑V / ESXi mismatch

    Azure AD Connect failures

    OOB exposure

    Terraform state corruption

Operational Risks

    Configuration drift

    Lack of rollback points

    Overlapping tasks

    Device state uncertainty

    Hardware failure

Security Risks

    PKI key exposure

    AD attack surface

    OOB misplacement

    ADFS/WAP exposure

    PAW contamination

Project Management Risks

    Scope creep

    Loss of structure

    Documentation gaps

    Branch mismanagement

Human Risks

    Fatigue

    Assuming knowledge

    Rushing steps

    Overconfidence

10. Mitigation Strategy

    Strict documentation discipline

    Overview → scope → outcome

    Document before configuring

    VM snapshots

    Verify Cisco configs

    Protect PKI keys

    Clean PAW usage

    Never assume device state

    Git feature‑branch workflow

    Maintain rollback points

11. Project Management Methodology

    Obsidian Kanban

    Granular tasks

    Single repo, multi‑branch

    Step‑by‑step execution

    No multi‑tasking

    Predictable structure

    Documentation‑first

    Enterprise‑grade discipline

12. Success Criteria

    Fully deployed hybrid identity

    Two‑tier PKI

    ADFS + WAP federation

    Azure AD Connect syncing

    Hyper‑V + ESXi aligned

    Cisco routing stable

    Terraform + PowerShell automation

    Git repo structured

    Documentation complete

    Architecture explainable in interviews

END OF DOCUMENT