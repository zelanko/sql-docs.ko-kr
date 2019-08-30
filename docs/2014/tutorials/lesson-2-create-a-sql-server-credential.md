---
title: '2단원: SQL Server 자격 증명 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: baa337d33173f292145d92b60d6192af2a716c5e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154335"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>2단원: SQL Server 자격 증명 만들기
  **자격 증명:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보를 저장하는 데 사용되는 개체입니다.  여기에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 프로세스는 자격 증명을 사용 하 여 Azure Blob 저장소 서비스에 인증 합니다. 자격 증명에는 스토리지 계정 이름과 스토리지 계정 **액세스 키** 값이 저장됩니다. 만든 자격 증명은 BACKUP/RESTORE 문을 실행할 때 WITH CREDENTIAL 옵션에 지정해야 합니다. 저장소 계정 **액세스 키**를 보고, 복사 하거나, 다시 생성 하는 방법에 대 한 자세한 내용은 [저장소 계정 액세스 키](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)를 참조 하세요.  
  
 자격 증명에 대한 자세한 내용은 [자격 증명](../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.  
  
 자격 증명이 사용되는 다른 예에 대한 정보는 [SQL Server 에이전트 프록시 만들기](../ssms/agent/create-a-sql-server-agent-proxy.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  아래에 설명 된 SQL Server 자격 증명을 만들기 위한 요구 사항은 SQL Server 백업 프로세스 ([URL에 백업 SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url.md)하 고 [Azure에 대 한 관리 되는 백업 SQL Server](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md))에만 적용 됩니다. Azure 스토리지에 액세스하여 백업을 쓰거나 읽을 때 SQL Server는 스토리지 계정 이름 및 액세스 키 정보를 사용합니다.  Azure storage에 데이터베이스 파일을 저장 하 [는 데 필요한 자격 증명을 만드는 방법에 대 한 자세한 내용은 3 단원: SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>SQL Server 자격 증명 만들기  
 SQL Server 자격 증명을 만들려면 다음 절차를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
  
2.  개체 탐색기에서 AdventureWorks2012 데이터베이스가 설치된 데이터베이스 엔진의 인스턴스에 연결하거나 이 자습서에서 사용할 자신의 데이터베이스를 사용합니다.  
  
3.  **표준** 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
4.  다음 예를 복사하여 쿼리 창에 붙여 넣고 필요한 대로 수정합니다.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![저장소 계정을 sql 자격 증명에 매핑](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "저장소 계정을 sql 자격 증명에 매핑")  
  
5.  T-SQL 문을 확인하고 **실행**을 클릭합니다.  
  
 백업 개념 및 요구 사항에 대 한 Azure Blob storage 서비스에 대 한 자세한 내용은 [SQL Server 백업 및 복원 Azure Blob Storage 서비스](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)를 참조 하세요.  
  
### <a name="next-lesson"></a>다음 단원  
 [3단원: Azure Blob Storage 서비스](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)에 전체 데이터베이스 백업을 작성 합니다.  
  
  
