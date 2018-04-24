---
title: '자습서: SQL Server 2016에서 Azure Blob Storage 서비스 사용 | Microsoft 문서'
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 328214976c50ff07b92376ae8061f97870980b24
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>자습서: SQL Server 2016에서 Azure Blob Storage 서비스 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Microsoft Azure Blob Storage 서비스에서 SQL Server 2016 사용 자습서를 시작합니다. 이 자습서는 SQL Server 데이터 파일 및 SQL Server 백업에 Microsoft Azure Blob Storage 서비스를 사용하는 방법을 이해하는 데 도움이 됩니다.  
  
Microsoft Azure Blob Storage 서비스에 대한 SQL Server 통합 지원은 SQL Server 2012 서비스 팩 1 CU2 향상된 기능으로 시작되었으며, SQL Server 2014 및 SQL Server 2016에서 더욱 개선되었습니다. 이 기능에 대한 개요 및 사용할 경우의 이점은 [Microsoft Azure의 SQL Server 데이터 파일](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)을 참조하세요. 라이브 데모는 [지정 시간 복원 데모](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)를 참조하세요.  
  
  
**다운로드**<br /><br />**>>**[!INCLUDE[ssSQL15](../includes/sssql15-md.md)]를 다운로드하려면 **[평가 센터](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)** 로 이동하세요.<br /><br />**>>** Azure 계정이 있으세요?  계정이 있는 경우 **[여기](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** 로 이동하여 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 이 이미 설치된 가상 컴퓨터를 실행해 보세요.  
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 여러 단원을 통해 Microsoft Azure Blob Storage 서비스에서 SQL Server 데이터 파일을 사용하는 방법을 보여 줍니다. 각 단원은 특정 작업을 중심으로 하며, 단원을 순서대로 완료해야 합니다. 먼저 저장된 액세스 정책과 공유 액세스 서명을 사용하여 Blob Storage에 새 컨테이너를 만드는 방법을 알아봅니다. 그런 다음 SQL Server 자격 증명을 만들어 Azure Blob Storage에 SQL Server를 통합하는 방법을 살펴봅니다. 데이터베이스를 Blob Storage에 백업하고 Azure 가상 컴퓨터에 복원합니다. SQL Server 2016 파일-스냅숏 트랜잭션 로그 백업을 사용하여 특정 시점 및 새 데이터베이스로 복원합니다. 최종적으로, 이 자습서에서는 파일-스냅숏 백업 이해와 작업에 도움이 되도록 메타데이터 시스템 저장 프로시저 및 함수를 사용하는 방법을 보여 줍니다.  
  
이 문서에서는 다음을 가정합니다.  
  
-   AdventureWorks2014의 복사본이 설치된 SQL Server 2016의 온-프레미스 인스턴스가 있습니다.  
  
-   Azure Storage 계정이 있습니다.  
  
-   SQL Server 2016이 설치된 Azure 가상 컴퓨터가 하나 이상 있으며, [Azure에서 SQL Server 가상 컴퓨터 프로비전](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-provision-sql-server/)에 따라 이 가상 컴퓨터를 프로비전했습니다. 필요에 따라 [8단원. 로그 백업에서 새 데이터베이스로 복원](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)의 시나리오를 위해 두 번째 가상 컴퓨터를 사용할 수 있습니다.  
  
이 자습서는 다음 9개의 단원으로 구성되어 있으며, 순서대로 완료해야 합니다.  
  
**[1단원: Azure 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명 만들기](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
이 단원에서는 새 Blob 컨테이너에 정책을 만들고, SQL Server 자격 증명을 만드는 데 사용할 공유 액세스 서명도 생성합니다.  
  
**[2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
이 단원에서는 Microsoft Azure Storage 계정에 액세스하는 데 사용되는 보안 정보를 저장하기 위해 SAS 키를 사용하여 자격 증명을 만듭니다.  
  
**[3단원: URL에 데이터베이스 백업](../relational-databases/lesson-3-database-backup-to-url.md)**  
이 단원에서는 온-프레미스 데이터베이스를 Microsoft Azure Blob Storage에 백업합니다.  
  
**[4단원: URL에서 가상 컴퓨터로 데이터베이스 복원](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
이 단원에서는 Microsoft Azure Blob Storage에서 Azure 가상 컴퓨터로 데이터베이스를 복원합니다.  
  
**[5단원: 파일-스냅숏 백업을 사용하여 데이터베이스 백업](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)**  
이 단원에서는 파일-스냅숏 백업 및 뷰-파일 스냅숏 메타데이터를 사용하여 데이터베이스를 백업합니다.  
  
**[6단원: 파일-스냅숏 백업을 사용하여 작업 및 백업 로그 생성](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
이 단원에서는 데이터베이스에 작업을 생성하고 파일-스냅숏 백업 및 뷰-파일 스냅숏 메타데이터를 사용하여 여러 로그 백업을 수행합니다.  
  
**[7단원: 데이터베이스를 특정 시점으로 복원](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
이 단원에서는 두 개의 파일-스냅숏 로그 백업을 사용하여 데이터베이스를 특정 시점으로 복원합니다.  
  
**[8단원. 로그 백업에서 새 데이터베이스로 복원](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)**  
이 단원에서는 파일-스냅숏 로그 백업에서 다른 가상 컴퓨터의 새 데이터베이스로 복원합니다.  
  
**[9단원: 백업 세트 및 파일-스냅숏 백업 관리](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)**  
이 단원에서는 불필요한 백업 세트를 삭제하고 분리된 파일 스냅숏 백업(있는 경우)을 삭제하는 방법을 알아봅니다.  
  
## <a name="see-also"></a>참고 항목  
[Microsoft Azure의 SQL Server 데이터 파일](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Azure의 데이터베이스 파일에 대한 파일-스냅숏 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[URL에 대한 SQL Server 백업](../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
  

