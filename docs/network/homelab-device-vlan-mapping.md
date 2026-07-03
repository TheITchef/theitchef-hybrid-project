| Device  | Role        | VLAN ID | Notes              |
|---------|------------|---------|--------------------|
| DC01    | Identity    | 10      | AD DS, PKI, ADFS   |
| MS01    | VM host     | 30      | App / infra VMs    |
| ESXi01  | Hypervisor  | 20      | mgmt + vMotion     |
| ESXi02  | Hypervisor  | 20      | mgmt + vMotion     |
| PN52    | PAW         | 99      | Admin workstation  |
| T470s   | PAW         | 99      | Admin workstation  |
| 3560CG  | OOB switch  | 100     | mgmt interfaces    |
| 891F    | Router      | 90      | Inside interface   |
