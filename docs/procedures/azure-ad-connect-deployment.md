# Azure AD Connect Deployment Procedure
## Last Updated: 2026‑07‑05

---

## 1. Overview
This procedure describes the deployment of **Azure AD Connect** to synchronize on‑premises Active Directory (**theitchef.com**) with Azure Active Directory.  
It follows the project’s documentation‑first workflow and prepares the environment for future federation (ADFS) and modern authentication.

---

## 2. Scope
This procedure covers:
- Preparing the Azure AD Connect server (Hyper‑V VM)
- Installing Azure AD Connect
- Configuring Full Sync (Password Hash Sync)
- Enabling Hybrid Join
- Validating synchronization
- Documenting configuration

---

## 3. Prerequisites
- AD DS domain **theitchef.com** fully deployed  
- DNS resolution between on‑prem and Azure  
- Verified PAW reachability  
- Azure tenant ready  
- Global Administrator credentials  
- Enterprise Admin credentials  
- Documented network state  
- VM snapshot created before installation  

---

## 4. Deployment Steps

### 4.1 Prepare the Azure AD Connect Server
- Deploy Windows Server VM on Hyper‑V  
- Assign static IP  
- Join **theitchef.com** domain  
- Install all updates  
- Verify connectivity to Azure endpoints  
- Snapshot the VM  

### 4.2 Download Azure AD Connect
- Download from Microsoft  
- Verify checksum  
- Store installer in `assets/exports/`  

### 4.3 Install Azure AD Connect
- Run installer  
- Choose **Customize**  
- Select **Password Hash Sync**  
- Enable **Hybrid Azure AD Join**  
- Provide Azure Global Admin credentials  
- Provide Enterprise Admin credentials  
- Select correct OU filtering  
- Configure staging mode (optional)  

### 4.4 Configure Sync Options
- Password Hash Sync  
- Device Sync  
- Group filtering (if required)  
- Attribute filtering (default recommended)  
- Verify scheduler enabled  

### 4.5 Validate Synchronization
- Run initial sync  
- Check Azure AD Connect Health  
- Validate users appear in Azure AD  
- Validate devices appear in Azure AD  
- Validate hybrid join  
- Document sync cycle  

---

## 5. Verification
- `Start-ADSyncSyncCycle -PolicyType Delta`  
- Azure AD Connect Health portal  
- Azure AD user/device list  
- Event Viewer logs  
- PAW login test  
- Azure portal sign‑in logs  

---

## 6. Deliverables
- Azure AD Connect installed  
- Full Sync configured  
- Hybrid Join enabled  
- Sync validated  
- Documentation stored under `docs/procedures/`  
- VM snapshot post‑deployment  

---

## 7. Acceptance Criteria
- Sync runs without errors  
- Users appear in Azure AD  
- Devices appear in Azure AD  
- Hybrid Join validated  
- Documentation complete  
- Branch merged and deleted  

---

## 8. References
- [[AD DS Deployment Procedure]]  
- [[Risk Assessment]]  
- [[Project Charter]]  
- [[Current State Assessment]]  
