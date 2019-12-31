---
title: Manage DQS Databases
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 655a67aa-d662-42f2-b982-c6217125ada8
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ce7b0239168a0a85e5d0f559b042dac0562ead94
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246983"
---
# <a name="manage-dqs-databases"></a>Manage DQS Databases

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 섹션에서는 백업/복원 또는 분리/연결과 같이 DQS 데이터베이스에서 수행할 수 있는 데이터베이스 관리 작업에 대한 정보를 제공합니다.  
  
##  <a name="BackupRestore"></a>DQS 데이터베이스 백업 및 복원  
 SQL Server 데이터베이스 백업 및 복원은 데이터베이스 관리자가 재해 복구 시 백업 데이터베이스에서 데이터를 복구하여 데이터 손실을 방지하기 위해 수행하는 일반적인 작업입니다. [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]는 주로 두 개의 SQL Server 데이터베이스인 DQS_MAIN 및 DQS_PROJECTS에 의해 구현 됩니다. DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] ) 데이터베이스의 백업 및 복원 절차는 다른 SQL Server 데이터베이스의 경우와 비슷합니다. DQS 데이터베이스의 백업 및 복원을 수행할 때는 다음과 같은 세 가지 점에 주의해야 합니다.  
  
-   DQS 데이터베이스의 백업 및 복원 작업이 동기화되어야 합니다. 그렇지 않으면 복원된 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 가 작동하지 않습니다.  
  
-   DQS 데이터베이스 DQS_MAIN과 DQS_PROJECTS에는 단순 데이터베이스 개체(예: 테이블 및 저장 프로시저) 외에도 어셈블리 및 기타 복잡한 개체가 포함되어 있습니다.  
  
-   DQS 데이터베이스가 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]로 작동하기 위해 필요한 몇몇 외부 엔터티가 있습니다. 구체적으로 말하면 master 데이터베이스의 SQL Server 로그인 2개(##MS_dqs_db_owner_login## 및 ##MS_dqs_service_login##)와 초기화 저장 프로시저(DQInitDQS_MAIN)입니다.  
  
 SQL Server의 백업 및 복원에 대한 자세한 내용은 [SQL Server 데이터베이스 백업 및 복원](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하십시오.  
  
### <a name="default-autogrowth-size-and-recovery-model-for-the-dqs-databases"></a>DQS 데이터베이스에 대한 기본 자동 증가 크기 및 복구 모델  
 DQS 데이터베이스 및 트랜잭션 로그가 무제한으로 커져서 잠재적으로 하드 디스크를 가득 채우지 않도록 하려면  
  
-   DQS 데이터베이스의 기본 **자동 증가** 크기는 10%로 설정됩니다.  
  
-   DQS 데이터베이스의 기본 복구 모델은 **단순**으로 설정됩니다. 단순 복구 모델에서 트랜잭션은 최소한으로 기록되며, 로그 잘림은 트랜잭션 로그(.ldf 파일)에서 공간을 확보하기 위해 트랜잭션이 완료된 후에 자동으로 발생합니다. 단순 복구 모델에 대한 자세한 내용은 [전체 데이터베이스 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]
>  -   단순 복구 모델에서는 오랜 시간 동안 로그 레코드가 활성 상태로 유지되는 경우(예: 길고 시간이 많이 소요되는 트랜잭션) 로그 잘림이 지연될 수 있으므로 트랜잭션 로그가 가득 찰 수 있습니다. 또한 로그 잘림을 수행하더라도 물리적 로그 파일(.ldf 파일)의 크기는 줄어들지 않습니다. 물리적 로그 파일의 크기를 줄이려면 로그 파일을 축소해야 합니다. 트랜잭션 로그와 관련된 문제를 해결하는 방법에 대한 자세한 내용은 [](../relational-databases/logs/the-transaction-log-sql-server.md)[의 https://go.microsoft.com/fwlink/?LinkId=237446트랜잭션 로그&#40;SQL Server&#41;](https://go.microsoft.com/fwlink/?LinkId=237446) 또는 Microsoft 지원 아티클을 참조하세요.  
> -   데이터에 대해 지정 시간 복구를 수행하려면 DQS 데이터베이스에 대해 전체 백업 또는 차등 백업을 정기적으로 수행하고 트랜잭션 로그도 백업해야 합니다. 자세한 내용은 [전체 데이터베이스 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md) 및 [트랜잭션 로그 백업&#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)을 참조하세요.  
  
##  <a name="DetachAttach"></a>DQS 데이터베이스 분리/연결  
 DQS 데이터베이스를 같은 컴퓨터의 다른 SQL Server 인스턴스로 변경하거나 데이터베이스를 이동하려는 경우 DQS 데이터베이스의 데이터 및 트랜잭션 로그 파일을 분리한 다음 SQL Server의 같은 인스턴스나 다른 인스턴스에 데이터베이스를 다시 연결할 수 있습니다.  
  
 SQL Server에서 데이터베이스를 분리 및 연결하기 전에 고려해야 할 사항은 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|DQS 데이터베이스를 백업 및 복원하는 방법에 대해 설명합니다.|[DQS 데이터베이스 백업 및 복원](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|DQS 데이터베이스를 분리 및 연결하는 방법을 설명합니다.|[DQS 데이터베이스 분리 및 연결](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>참고 항목  
 [DQS 관리](../data-quality-services/dqs-administration.md)  
  
  
