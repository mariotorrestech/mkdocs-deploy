# Diagram Examples

## Flowcharts

```mermaid
graph LR
  A[Start] --> B{Failure?};
  B -->|Yes| C[Investigate...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Success!];
```

AND THIS:

## Sequence Diagrams

```mermaid
sequenceDiagram
  autonumber
  Server->>Terminal: Send request
  loop Health
      Terminal->>Terminal: Check for health
  end
  Note right of Terminal: System online
  Terminal-->>Server: Everything is OK
  Terminal->>Database: Request customer data
  Database-->>Terminal: Customer data
```

AND THIS:

```mermaid
graph TD
    subgraph Lab Network - 10.0.3.0/24
        DC[Domain Controller<br>Windows Server 2019]
        WS1[Workstation 1<br>Windows 10]
        WS2[Workstation 2<br>Windows 11]
        SVR[File Server<br>Windows Server 2019]
        VULN[Vulnerable Server<br>Windows Server 2016]
        KALI[Kali Linux<br>Attack Machine]
    end
    
    DC --- WS1
    DC --- WS2
    DC --- SVR
    DC --- VULN
    KALI -.- DC
    KALI -.- WS1
    KALI -.- WS2
    KALI -.- SVR
    KALI -.- VULN
```

## Environment Components

## Domain Infrastructure

- **Domain Name**: MARVEL
- **Forest/Domain Functional Level**: Windows Server 2016
- **Domain Controller**: Windows Server 2019
  - Roles: AD DS, DNS, DHCP

## Client Systems

| System    | OS             | IP         | Purpose          |
| --------- | -------------- | ---------- | ---------------- |
| Punisher  | Windows 10 Pro | 10.0.3.100 | User workstation |
| Spiderman | Windows 10 Pro | 10.0.3.101 | User workstation |

## Server Systems

| System            | OS                  | IP        | Purpose                     |
| ----------------- | ------------------- | --------- | --------------------------- |
| Domain Controller | Windows Server 2019 | 10.0.3.10 | File shares, sensitive data |
