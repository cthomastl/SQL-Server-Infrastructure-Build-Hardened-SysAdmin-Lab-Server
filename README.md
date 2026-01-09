SQL Server Infrastructure Build & Hardened SysAdmin Lab
 Server: dbsql01 | Role: Database Systems Administration

1. Project Overview
This project demonstrates professional-level System Administration by building a hardened, high-performance SQL Server 2022 environment from scratch. Key milestones include manual virtual hardware provisioning, RAID 1 storage engineering, and implementing a strict "Least Privilege" security model through Active Directory service accounts and NTFS permissions.

2. Advanced Storage Engineering & RAID 1 Configuration
A critical SysAdmin task is ensuring that data survives hardware failure. I moved beyond standard "Simple Volumes" to a redundant, optimized storage architecture.

Virtual Hardware Provisioning
SCSI Controller Management: I manually added and configured multiple SCSI Controllers to isolate OS, Data, and Log traffic for maximum throughput.

Hardware Expansion: Provisioned additional 100GB VHDX virtual hard drives and "hot-plugged" them into the VM's virtual motherboard via Hyper-V Settings.

Disk Initialization & Mirroring
GPT Initialization: Used the GPT (GUID Partition Table) partition style for all new disks to ensure support for modern volume sizes and partition integrity.

RAID 1 Implementation: To prevent data loss, I converted disks from Basic to Dynamic and created a New Mirrored Volume (RAID 1). This ensures real-time data duplication across two physical disk files.

SQL Alignment (64K Blocks): During formatting, I manually overrode the default 4K cluster size in favor of a 64K Allocation Unit Size. This is a standard SysAdmin optimization that aligns the file system with SQL Server's 64KB I/O patterns to reduce disk latency.

<img width="584" height="380" alt="InitiazlizedDisk" src="https://github.com/user-attachments/assets/a458c42c-c013-4dcd-8428-2b59c2168c03" />


3. Security Hardening & Permissions Assignment
Security is the cornerstone of System Administration. I hardened this server by removing administrative dependencies and locking down the file system.

Least Privilege Identity Model
Service Account Creation: Migrated the SQL Server engine from the high-privilege "Local System" account to a dedicated, low-privilege domain account: svc_sql@oakmont.org.

Granular NTFS Permissions
Permission Assignment: I manually configured the Security/NTFS permissions for the new SQLData (D:) drive.

Access Control: I granted the svc_sql account Full Control over its specific data directories while ensuring no other non-admin users could access the database files.

<img width="203" height="204" alt="GaveSVC_SQLaccesstoDBfolder" src="https://github.com/user-attachments/assets/f3fa274b-f38d-4c59-8ca1-86afb656cbee" />


4. Logical & Physical Data Separation
A key SysAdmin best practice is separating the "System" from the "Data."

Database Relocation: Successfully performed a physical move of the HR_Database files from the OS drive (C:) to the newly engineered RAID mirror (D:).

Path Validation: Verified the SQL Server engine could successfully read and write to the new path: D:\SQLData\Data\.

<img width="592" height="348" alt="HRDBfilesmovestoDdataDrive" src="https://github.com/user-attachments/assets/6e6d7e89-9dff-4cad-bc5a-6b9aac5e5544" />




5. SysAdmin Skillset Summary
Virtualization: Expertise in Hyper-V, SCSI Controller management, and VHDX provisioning.

Storage Ops: Proficient in RAID 1, GPT initialization, and 64K block-level optimization.

Security Ops: Advanced knowledge of Active Directory service accounts and granular NTFS permission management.
