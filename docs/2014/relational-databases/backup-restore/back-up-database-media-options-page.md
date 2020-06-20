---
title: 데이터베이스 백업(미디어 옵션 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- swb.backupdatabase.mediaoptions.f1
- sql12.swb.backupdatabase.mediaoptions.f1
ms.assetid: eff36228-710c-4ed5-9af5-95859575dc0f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cd09eb091a7f488f891bc2e69d19ad039b65e065
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959621"
---
# <a name="back-up-database-media-options-page"></a>데이터베이스 백업(미디어 옵션 페이지)
  **데이터베이스 백업** 대화 상자의 **미디어 옵션** 페이지를 사용하여 데이터베이스 미디어 옵션을 확인하거나 수정할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 백업을 만들려면**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  데이터베이스 유지 관리 계획을 정의하여 데이터베이스 백업을 만들 수 있습니다. 자세한 내용은 [유지 관리 계획](../maintenance-plans/maintenance-plans.md) 및 [유지 관리 계획 마법사 사용](../maintenance-plans/use-the-maintenance-plan-wizard.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 태스크를 지정할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)][스크립트](/sql/t-sql/statements/backup-transact-sql) 단추를 클릭한 다음 스크립트에 대한 대상을 선택하여 해당되는 **BACKUP** 스크립트를 생성할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
### <a name="overwrite-media"></a>미디어 덮어쓰기  
 **미디어 덮어쓰기** 패널의 옵션은 백업이 미디어에 쓰여지는 방법을 제어합니다. URL(Azure Storage)을 데이터베이스 백업 대화 상자의 일반 페이지에 있는 백업 대상으로 선택한 경우 미디어 덮어쓰기 섹션의 옵션을 사용할 수 없습니다. `BACKUP TO URL.. WITH FORMAT` Transact-SQL 문을 사용하여 백업을 덮어쓸 수 있습니다. 자세한 내용은 [URL에 대한 SQL Server Backup](sql-server-backup-to-url.md)을 참조하세요.  
  
 **새 미디어에 백업하고 기존 백업 세트 모두 지우기** 옵션만 암호화 옵션과 함께 지원됩니다. **기존 미디어에 백업** 섹션의 옵션을 선택하는 경우 **백업 옵션** 페이지의 암호화 옵션을 사용할 수 없게 됩니다.  
  
> [!NOTE]  
>  미디어 세트에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)인스턴스를 실행하는 컴퓨터에 테이프 드라이브가 연결되어 있는 경우에만 사용할 수 있습니다.  
  
 **기존 미디어 세트에 백업**  
 데이터베이스를 기존 미디어 세트에 백업합니다. 이 옵션 단추를 선택하면 세 개의 옵션이 활성화됩니다.  
  
 다음 옵션 중 하나를 선택합니다.  
  
 **기존 백업 세트에 추가**  
 모든 이전 백업을 유지하면서 백업 세트를 기존 미디어 세트에 추가합니다.  
  
 **기존 백업 세트 모두 덮어쓰기**  
 기존 미디어 세트의 모든 이전 백업을 현재 백업으로 바꿉니다.  
  
 **미디어 세트 이름 및 백업 세트 만료 확인**  
 상황에 따라 기존 미디어 세트로 백업할 경우 백업 세트의 만료 날짜 및 이름을 식별하기 위해 백업 작업이 필요할 수 있습니다.  
  
 **미디어 세트 이름**  
 **미디어 세트 이름 및 백업 세트 만료 확인** 을 선택한 경우 필요에 따라 이 백업 작업에 사용되는 미디어 세트 이름을 지정합니다.  
  
 **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
 이전 백업 세트를 지우고 새 미디어 세트를 사용합니다.  
  
 이 옵션을 클릭하면 다음 옵션이 활성화됩니다.  
  
 **새 미디어 세트 이름**  
 필요에 따라 미디어 세트의 새 이름을 입력합니다.  
  
 **새 미디어 세트 설명**  
 필요에 따라 새 미디어 세트에 대한 이해하기 쉬운 설명을 입력합니다. 이 설명은 내용을 정확하게 전달할 수 있을 만큼 구체적이어야 합니다.  
  
### <a name="reliability"></a>안정성  
 **트랜잭션 로그** 패널의 옵션은 백업 작업으로 오류 관리를 제어합니다.  
  
 **완료 시 백업 확인**  
 백업 세트가 올바른지 확인하고 모든 볼륨을 읽을 수 있는지 확인합니다.  
  
 **미디어에 쓰기 전에 체크섬 수행**  
 백업 미디어에 쓰기 전에 체크섬을 확인합니다. 이 옵션을 선택하는 것은 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 BACKUP 문에서 CHECKSUM 옵션을 지정하는 것과 같습니다. 이 옵션을 선택하면 작업이 증가하여 백업 작업의 백업 처리량이 줄어들 수 있습니다. 백업 체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
 **오류 발생 시 계속**  
 하나 이상의 오류가 발생한 다음에도 백업 작업이 계속됩니다.  
  
### <a name="transaction-log"></a>트랜잭션 로그  
 **트랜잭션 로그** 패널의 옵션은 트랜잭션 로그 백업의 동작을 제어합니다. 이러한 옵션은 전체 복구 모델 또는 대량 로그 복구 모델에서만 해당됩니다. **트랜잭션 로그** 가 **데이터베이스 백업** 대화 상자의 [일반](../../integration-services/general-page-of-integration-services-designers-options.md) 페이지에 있는 **백업 유형** 필드에서 선택된 경우에만 이 옵션이 활성화됩니다.  
  
> [!NOTE]  
>  트랜잭션 로그 백업에 대한 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)을 참조하세요.  
  
 **트랜잭션 로그 잘라내기**  
 트랜잭션 로그를 백업한 다음 잘라 로그 공간을 확보합니다. 데이터베이스는 온라인 상태로 유지됩니다. 기본 옵션입니다.  
  
 **비상 로그 백업을 수행하고 복원 중인 상태로 데이터베이스 유지**  
 비상 로그 백업을 수행하고 데이터베이스를 복원 상태로 둡니다. 이 옵션을 사용하여 일반적으로 데이터베이스 복원 준비 과정에서 백업되지 않은 로그(활성 로그)를 백업하는 *비상 로그 백업*을 만들 수 있습니다. 데이터베이스가 완전히 복원되기 전까지는 데이터베이스를 사용할 수 없습니다.  
  
 이 옵션을 선택하는 것은 [BACKUP](/sql/t-sql/statements/backup-transact-sql) 문([!INCLUDE[tsql](../../includes/tsql-md.md)])에서 WITH NO_TRUNCATE, NORECOVERY를 지정하는 것과 같습니다. 자세한 내용은 [비상 로그 백업&#40;SQL Server&#41;](tail-log-backups-sql-server.md)을 참조하세요.  
  
### <a name="tape-drive"></a>테이프 드라이브  
 **테이프 드라이브** 패널의 옵션은 백업 작업 동안 테이프 관리를 제어합니다. **테이프** 가 **데이터베이스 백업** 대화 상자의 [일반](../../integration-services/general-page-of-integration-services-designers-options.md) 페이지에 있는 **대상** 필드에서 선택된 경우에만 이 옵션이 활성화됩니다.  
  
> [!NOTE]  
>  테이프 디바이스를 사용하는 방법은 [백업 디바이스&#40;SQL Server&#41;](backup-devices-sql-server.md)를 참조하세요.  
  
 **백업 후 테이프 언로드**  
 백업이 완료된 후 테이프를 언로드합니다.  
  
 **언로드 전에 테이프 되감기**  
 테이프를 언로드하기 전에 되감습니다. **백업 후 테이프 언로드** 를 선택한 경우에만 이 옵션을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
