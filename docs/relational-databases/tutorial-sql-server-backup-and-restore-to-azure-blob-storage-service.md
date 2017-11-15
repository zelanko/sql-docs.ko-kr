---
title: "Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원 | Microsoft 문서"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016 Preview
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a59c1224d71e9c8a8626c325dbef600c19078e38
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>자습서: Azure Blob Storage Service로 SQL Server 백업 및 복원
이 자습서는 Azure Blob Storage 서비스에서 백업을 작성하고 복원하는 방법을 이해하도록 도와줍니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 저장소 계정과 blob 컨테이너를 만들어서 저장소 계정에 액세스할 자격 증명을 만들고 Blob Service에 백업을 작성하며 간단한 복원을 수행할 수 있는 방법을 보여 줍니다. 이 자습서는 다음 네 단원으로 이루어져 있습니다.  
  
[1단원: Azure 저장소 개체 만들기](http://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5)  
이 단원에서는 Azure 저장소 계정 및 blob 컨테이너를 만듭니다.  
  
[2단원: SQL Server 자격 증명 만들기](http://msdn.microsoft.com/library/64f8805c-1ddc-4c96-a47c-22917d12e1ab)  
이 단원에서는 Azure 저장소 계정에 액세스하는 데 사용하는 보안 정보를 저장하는 자격 증명을 만들 수 있습니다.  
  
[3단원: Azure Blob Storage Service로 전체 데이터베이스 백업 작성](http://msdn.microsoft.com/library/454c8296-64e9-46ed-b141-5ebfbc8a4fe2)  
이 단원에서는 Azure Blob Storage 서비스에 AdventureWorks2012 데이터베이스 백업을 작성하는 T-SQL 문을 실행합니다.  
  
[4단원: 전체 데이터베이스 백업에서 복원 수행](http://msdn.microsoft.com/library/580f76e6-9802-4abc-9043-db6de592c733)  
이 단원에서는 이전 단원에서 만든 데이터베이스 백업에서 복원하는 T-SQL 문을 실행합니다.  
  
### <a name="requirements"></a>요구 사항  
이 자습서를 완료하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 개념과 T-SQL 구문에 대해 잘 알고 있어야 합니다. 이 자습서를 사용하려면 다음과 같은 시스템 요구 사항을 만족해야 합니다.  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 인스턴스와 AdventureWorks2012 데이터베이스가 설치되었습니다.  
  
    SQL Server 인스턴스는 온-프레미스 또는 Azure 가상 컴퓨터에 있을 수 있습니다.  
  
    AdventureWorks2012 대신 사용자 데이터베이스를 사용하고 tsql 구문을 적절하게 수정할 수 있습니다.  
  
-   BACKUP 또는 RESTORE 명령을 실행하는 데 사용되는 사용자 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다.  
  
### <a name="additional-reading"></a>더 보기  
다음은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업에 Azure Blob Storage 서비스를 사용할 때 개념 및 최선의 구현 방법을 이해하기 위한 권장 참조 항목입니다.  
  
1.  [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
## <a name="see-also"></a>참고 항목  
[Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

