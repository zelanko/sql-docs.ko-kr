---
title: '자습서: SQL Server 백업 및 복원 Windows azure Blob Storage 서비스 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2216674bec52dd4d4800aa1b03aa4a2834667974
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62524053"
---
# <a name="tutorial-sql-server-backup-and-restore-to-windows-azure-blob-storage-service"></a>자습서: Microsoft Azure Blob Storage Service로 SQL Server 백업 및 복원
  SQL Server 백업 및 Windows Azure Blob Storage 서비스로 복원 시작 자습서를 시작합니다. 이 자습서는 Windows Azure Blob 스토리지 서비스에서 백업을 작성하고 복원하는 방법을 이해하도록 도와 줍니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 Windows 스토리지 계정과 blob 컨테이너를 만들어서 스토리지 계정에 액세스할 자격 증명을 만들고 Blob 서비스에 백업을 작성하며 간단한 복원을 수행할 수 있는 방법을 보여 줍니다. 이 자습서는 다음 네 단원으로 이루어져 있습니다.  
  
 [1단원: Windows Azure 저장소 개체 만들기](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 이 단원에서는 Windows Azure 스토리지 계정 및 blob 컨테이너를 만듭니다.  
  
 [2단원: SQL Server 자격 증명 만들기](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 이 단원에서는 Windows Azure 스토리지 계정에 액세스하는 데 사용하는 보안 정보를 저장하는 자격 증명을 만들 수 있습니다.  
  
 [3단원: Windows Azure Blob Storage 서비스에 전체 데이터베이스 백업을 작성합니다](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 이 단원에서는 Windows Azure Blob 스토리지 서비스에 AdventureWorks2012 데이터베이스 백업을 작성하는 T-SQL 문을 실행합니다.  
  
 [4단원: 전체 데이터베이스 백업에서 복원 수행](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 이 단원에서는 이전 단원에서 만든 데이터베이스 백업에서 복원하는 T-SQL 문을 실행합니다.  
  
### <a name="requirements"></a>요구 사항  
 이 자습서를 완료하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 개념과 T-SQL 구문에 대해 잘 알고 있어야 합니다. 이 자습서를 사용하려면 다음과 같은 시스템 요구 사항을 만족해야 합니다.  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]인스턴스와 AdventureWorks2012 데이터베이스가 설치되었습니다.  
  
     SQL Server 인스턴스는 온-프레미스 또는 Microsoft Azure 가상 머신에 있을 수 있습니다.  
  
     AdventureWorks2012 대신 사용자 데이터베이스를 사용하고 tsql 구문을 적절하게 수정할 수 있습니다.  
  
-   BACKUP 또는 RESTORE 명령을 실행하는 데 사용되는 사용자 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다.  
  
### <a name="additional-reading"></a>더 보기  
 다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업에 Windows Azure Blob 스토리지 서비스를 사용할 때 개념 및 최선의 구현 방법을 이해하기 위한 권장 참조 항목입니다.  
  
1.  [Windows Azure Blob Storage 서비스로 SQL Server 백업 및 복원](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
