# ADFS Deployment Procedure
## Last Updated: 2026‑07‑06

---

## 1. Overview
This procedure describes the deployment of **Active Directory Federation Services (ADFS)** for hybrid identity federation between **theitchef.com** and Azure AD.  
It follows the documentation‑first workflow and ensures secure, predictable deployment of federation services.

---

## 2. Scope
This procedure covers:
- Preparing the ADFS server (Hyper‑V VM)
- Installing ADFS role
- Creating the federation farm
- Installing Web Application Proxy (WAP)
- Configuring SSL certificates
- Integrating ADFS with Azure AD
- Validating federation

---

## 3. Prerequisites
- AD DS domain **theitchef.com** fully deployed  
- Azure AD Connect operational  
- PKI issuing CA available  
- SSL certificate for `fs.theitchef.com`  
- DNS records prepared  
- Firewall rules prepared  
- WAP server reachable from DMZ  
- PAW ready for administrative tasks  
- VM snapshots created  

---

## 4. Deployment Steps

### 4.1 Prepare the ADFS Server
- Deploy Windows Server VM  
- Assign static IP  
- Join **theitchef.com** domain  
- Install updates  
- Snapshot VM  
- Verify DNS resolution  

### 4.2 Install ADFS Role
- Server Manager → Add Roles  
- Select **Active Directory Federation Services**  
- Restart if required  

### 4.3 Configure SSL Certificate
- Import certificate for `fs.theitchef.com`  
- Ensure private key is present  
- Bind certificate to HTTPS  
- Validate chain with PKI  

### 4.4 Create ADFS Farm
- Launch ADFS Configuration Wizard  
- Select **Create the first federation server in a federation server farm**  
- Provide domain admin credentials  
- Select SSL certificate  
- Set federation service name: **fs.theitchef.com**  
- Set federation service display name: **theitchef.com**  
- Complete configuration  

### 4.5 Prepare Web Application Proxy (WAP)
- Deploy WAP server in DMZ  
- Install Remote Access role  
- Install certificate for `fs.theitchef.com`  
- Configure WAP to point to ADFS  
- Provide ADFS admin credentials  
- Validate trust establishment  

### 4.6 Integrate ADFS with Azure AD
- Connect to Azure AD using Global Admin  
- Run: `Connect-MsolService`  
- Run: `Set-MsolDomainAuthentication -DomainName theitchef.com -FederationBrandName "theitchef.com" -Authentication Federated`  
- Validate federation metadata  
- Validate sign‑in logs  

---

## 5. Verification
- ADFS event logs  
- WAP event logs  
- Federation metadata URL  
- Azure AD sign‑in logs  
- Test login via ADFS  
- Validate token issuance  
- Validate certificate chain  

---

## 6. Deliverables
- ADFS farm deployed  
- WAP configured  
- SSL certificates installed  
- Federation metadata published  
- Azure AD federation enabled  
- Documentation stored under `docs/procedures/`  
- VM snapshots post‑deployment  

---

## 7. Acceptance Criteria
- ADFS sign‑ins successful  
- WAP trust established  
- Federation metadata reachable  
- Azure AD federation validated  
- Documentation complete  
- Branch merged and deleted  

---

## 8. References
- [[AD DS Deployment Procedure]]  
- [[Azure AD Connect Deployment Procedure]]  
- [[PKI Deployment Procedure]]  
- [[Risk Assessment]]  

