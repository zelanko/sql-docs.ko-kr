---
title: 데이터베이스 복원(옵션 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoredb.options.f1
ms.assetid: 9a75d48b-c25f-40f3-8ea1-32cfa8211754
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 266c127a8ef38a1a5701de24f9442861e604d84d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875639"
---
# <a name="restore-database-options-page"></a>데이터베이스 복원(옵션 페이지)
  **데이터베이스 복원** 대화 상자의 **옵션** 페이지를 사용하여 복원 작업의 동작 및 결과를 수정할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 백업을 복원하려면**  
  
-   [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
-   [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 복원 태스크를 지정할 때 이 복원 작업에 대해 RESTORE 문을 포함하는 해당 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 생성할 수 있습니다. 스크립트를 생성하려면 **스크립트** 를 클릭한 다음 스크립트 대상을 선택합니다. RESTORE 구문에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)를 참조하세요.  
  
## <a name="options"></a>변수  
  
### <a name="restore-options"></a>복원 옵션  
 복원 작업의 동작 측면을 수정하려면 **복원 옵션** 패널의 옵션을 사용합니다.  
  
 **기존 데이터베이스 덮어쓰기[WITH REPLACE]**  
 **데이터베이스 복원**대화 상자에 있는 [일반](../../integration-services/general-page-of-integration-services-designers-options.md) 페이지의 **복원 위치** 필드에서 지정하는 데이터베이스 이름을 현재 사용 중인 모든 데이터베이스의 파일을 복원 작업에서 덮어씁니다. 다른 데이터베이스에서 기존 데이터베이스 이름으로 백업을 복원하는 중이더라도 기존 데이터베이스의 파일을 덮어씁니다. 이 옵션을 선택하는 것은 [RESTORE](/sql/t-sql/statements/restore-statements-arguments-transact-sql) 문에서 REPLACE 옵션을 사용하는 것과 같습니다.([!INCLUDE[tsql](../../includes/tsql-md.md)]).  
  
> [!CAUTION]  
>  이 옵션은 신중하게 고려한 후에만 사용해야 합니다. 자세한 내용은 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)를 참조하세요.  
  
 **복제 설정 유지[WITH KEEP_REPLICATION]**  
 게시된 데이터베이스를 해당 데이터베이스가 생성된 서버 이외의 다른 서버로 복원할 경우 복제 설정을 유지합니다. 이 옵션은 백업을 만들 때 데이터베이스가 복제된 경우에만 해당합니다.  
  
 이 옵션은 RECOVERY 옵션을 사용하여 백업을 복원하는 것과 같은 **커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용할 수 있는 상태로 유지합니다.** 옵션(이 표의 뒷부분에서 설명)과 함께만 사용할 수 있습니다.  
  
 이 옵션을 선택하는 것은 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 문에서 KEEP_REPLICATION 옵션을 사용하는 것과 같습니다.  
  
 자세한 내용은 [복제된 데이터베이스 백업 및 복원](../replication/administration/back-up-and-restore-replicated-databases.md)을 참조하세요.  
  
 **복원된 데이터베이스에 대한 액세스 제한[WITH RESTRICTED_USER]**  
 **db_owner**, **dbcreator**또는 **sysadmin**의 멤버만 복원된 데이터베이스를 사용할 수 있도록 합니다.  
  
 이 옵션을 선택하는 것은 RESTORE 문에서 RESTRICTED_USER 옵션을 사용하는 것과 같습니다.  
  
### <a name="recovery-state"></a>복구 상태  
 저장 작업 후에 데이터베이스의 상태를 확인하려면 **복구 상태** 패널의 옵션 중 하나를 선택해야 합니다.  
  
 **RESTORE WITH RECOVERY**  
 **일반 페이지**의 [복원에 사용할 백업 세트](../../integration-services/general-page-of-integration-services-designers-options.md)표에서 선택된 최종 백업을 복원한 후에 데이터베이스를 복구합니다. 이는 기본 옵션이고 [RESTORE](/sql/t-sql/statements/restore-statements-arguments-transact-sql) 문([!INCLUDE[tsql](../../includes/tsql-md.md)])에서 WITH RECOVERY를 지정하는 것과 같습니다.  
  
> [!NOTE]  
>  전체 복구 모델 또는 대량 로그 복구 모델에서 모든 로그 파일을 지금 복원하는 경우에만 이 옵션을 선택합니다.  
  
 **RESTORE WITH NORECOVERY**  
 데이터베이스를 복원 상태로 유지합니다. 현재 복구 경로에서 추가 백업을 복원할 수 있습니다. 데이터베이스를 복구하려면 RESTORE WITH RECOVERY 옵션을 사용하여 복원 작업을 수행해야 합니다(이전 옵션 참조).  
  
 이 옵션은 RESTORE 문에서 WITH NORECOVERY를 지정하는 것과 같습니다.  
  
 이 옵션을 선택하면 **복제 설정 유지** 옵션을 사용할 수 없습니다.  
  
 **RESTORE WITH STANDBY**  
 제한된 읽기 전용 액세스로 데이터베이스를 사용할 수 있도록 데이터베이스를 대기 모드로 유지합니다. 이 옵션은 RESTORE 문에서 WITH STANDBY를 지정하는 것과 같습니다.  
  
 이 옵션을 선택하면 **대기 파일** 입력란에서 대기 파일을 지정해야 합니다. 대기 파일은 복구 결과를 취소합니다.  
  
 **대기 파일**  
 대기 파일을 지정합니다. 대기 파일을 찾아보거나 입력란에 해당 경로 이름을 직접 입력할 수 있습니다.  
  
### <a name="tail-log-backup"></a>비상 로그 백업  
 데이터베이스 복원과 함께 수행할 비상 로그 백업을 지정할 수 있습니다.  
  
 **복원 전에 비상 로그 백업 가져오기**  
 비상 로그 백업을 수행하도록 지정하려면 이 확인란을 선택합니다.  
  
> [!NOTE]  
>  [백업 시간대](backup-timeline.md) 대화 상자에서 선택한 시점에 비상 로그 백업이 필요한 경우에는 이 확인란이 자동으로 선택되며 선택 사항을 편집할 수 없습니다.  
  
 **백업 파일**  
 비상 로그에 대한 백업 파일을 지정합니다. 백업 파일을 찾아보거나 입력란에 해당 이름을 직접 입력할 수 있습니다.  
  
### <a name="server-connections"></a>서버 연결  
 기존 데이터베이스 연결을 닫을 수 있습니다.  
  
 **기존 연결 닫기**  
 데이터베이스에 대한 활성 연결이 있으면 복원 작업이 실패할 수 있습니다. **기존 연결 닫기** 옵션을 선택하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 데이터베이스 간의 모든 활성 연결을 닫습니다. 이 확인란을 선택하면 복원 작업을 수행하기 전에 데이터베이스가 단일 사용자 모드로 설정되고 복원 작업이 완료될 때 데이터베이스가 다중 사용자 모드로 설정됩니다.  
  
### <a name="prompt"></a>프롬프트  
 **각 백업 복원 전에 확인**  
 각 백업을 복원한 후 복원 순서를 계속할지 여부를 묻는 **복원 계속** 대화 상자를 표시합니다. 이 대화 상자는 다음 미디어 세트(알려진 경우)의 이름과 다음 백업 세트의 이름 및 설명을 표시합니다.  
  
 이 옵션을 지정하면 모든 백업을 복원한 후에 복원 순서를 일시 중지할 수 있습니다. 예를 들어 이 옵션은 서버에 테이프 디바이스가 하나만 있어 다양한 미디어 세트의 테이프를 교체해야 할 경우 특히 유용합니다. 계속할 준비가 되었으면 **확인**을 클릭합니다.  
  
 **아니요**를 클릭하여 복원 순서를 중단할 수 있습니다. 이렇게 하면 데이터베이스를 복원 중인 상태로 둡니다. 사용자 편의를 위해 **복원 계속** 대화 상자에 설명된 다음 백업으로 재개하여 복원 순서를 나중에 계속할 수 있습니다. 다음 백업 복원 절차는 다음과 같이 데이터나 트랜잭션 로그를 포함하는지 여부에 따라 달라집니다.  
  
-   다음 백업이 전체 백업 또는 차등 백업인 경우 **데이터베이스 복원** 태스크를 다시 사용합니다.  
  
-   다음 백업이 파일 백업인 경우 **파일 및 파일 그룹 복원**태스크를 사용합니다. 자세한 내용은 [파일 및 파일 그룹 복원&#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)을 참조하세요.  
  
-   다음 백업이 로그 백업인 경우 **트랜잭션 로그 복원** 태스크를 사용합니다. 트랜잭션 로그를 복원하여 복원 순서를 재개하는 방법은 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [장치에서 백업 복원&#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)   
 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [데이터베이스 복원&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
