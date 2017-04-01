---
title: "Tutorial: SQL Server Backup and Restore to Windows Azure Blob Storage Service | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016 Preview"
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Tutorial: SQL Server Backup and Restore to Windows Azure Blob Storage Service
SQL Server 백업 및 Windows Azure Blob 저장소 서비스로 복원 시작 자습서를 시작합니다. 이 자습서는 Windows Azure Blob 저장소 서비스에서 백업을 작성하고 복원하는 방법을 이해하도록 도와 줍니다.  
  
## 학습 내용  
이 자습서에서는 Windows 저장소 계정과 blob 컨테이너를 만들어서 저장소 계정에 액세스할 자격 증명을 만들고 Blob 서비스에 백업을 작성하며 간단한 복원을 수행할 수 있는 방법을 보여 줍니다. 이 자습서는 다음 네 단원으로 이루어져 있습니다.  
  
[1단원: Windows Azure 저장소 개체 만들기](../Topic/Lesson%201:%20Create%20Windows%20Azure%20Storage%20Objects.md)  
이 단원에서는 Windows Azure 저장소 계정 및 blob 컨테이너를 만듭니다.  
  
[Lesson 2: Create a SQL Server Credential](../Topic/Lesson%202:%20Create%20a%20SQL%20Server%20Credential.md)  
이 단원에서는 Windows Azure 저장소 계정에 액세스하는 데 사용하는 보안 정보를 저장하는 자격 증명을 만들 수 있습니다.  
  
[Lesson 3: Write a Full Database Backup to the Windows Azure Blob Storage Service](../Topic/Lesson%203:%20Write%20a%20Full%20Database%20Backup%20to%20the%20Windows%20Azure%20Blob%20Storage%20Service.md)  
이 단원에서는 Windows Azure Blob 저장소 서비스에 AdventureWorks2012 데이터베이스 백업을 작성하는 T-SQL 문을 실행합니다.  
  
[4 단원: 전체 데이터베이스 백업에서 복원 수행](../Topic/Lesson%204:%20Perform%20a%20Restore%20From%20a%20Full%20Database%20Backup.md)  
이 단원에서는 이전 단원에서 만든 데이터베이스 백업에서 복원하는 T-SQL 문을 실행합니다.  
  
### 요구 사항  
이 자습서를 완료 하려면를 잘 알고 있어야 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 개념과 T-SQL 구문입니다. 이 자습서를 사용하려면 다음과 같은 시스템 요구 사항을 만족해야 합니다.  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]인스턴스와 AdventureWorks2012 데이터베이스가 설치되었습니다.  
  
    SQL Server 인스턴스는 온-프레미스 또는 Windows Azure 가상 컴퓨터에 있을 수 있습니다.  
  
    AdventureWorks2012 대신 사용자 데이터베이스를 사용하고 tsql 구문을 적절하게 수정할 수 있습니다.  
  
-   BACKUP 또는 RESTORE 명령을 실행하는 데 사용되는 사용자 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다.  
  
### 더 보기  
다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업에 Windows Azure Blob 저장소 서비스를 사용할 때 개념 및 최선의 구현 방법을 이해하기 위한 권장 참조 항목입니다.  
  
1.  [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## 관련 항목:  
[데이터베이스 및 로그 백업](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#databaselog)  
[PRIMARY 파일 그룹의 전체 파일 백업 만들기](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#filegroups)  
[데이터베이스 복원 및 파일 이동](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md#restoredbwithmove)  
  
