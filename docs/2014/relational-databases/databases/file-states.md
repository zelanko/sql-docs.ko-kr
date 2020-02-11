---
title: 파일 상태 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- restoring file state [SQL Server]
- verifying file states
- current file states
- verifying filegroup states
- file states [SQL Server]
- online file state
- offline file state [SQL Server]
- viewing filegroup states
- viewing file states
- suspect file state
- recovering file state [SQL Server]
- current filegroup state
- recovery pending file state [SQL Server]
- displaying file states
- states [SQL Server], files
- displaying filegroup states
- defunct file state
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc37fbade038b39d6d05cb5b51ecc3e8ba405e2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62871576"
---
# <a name="file-states"></a>파일 상태
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 파일의 상태는 데이터베이스 상태와는 별도로 유지 관리됩니다. 파일은 항상 하나의 특정 상태에 있습니다. 예를 들어 ONLINE이나 OFFLINE 상태일 수 있습니다. 파일의 현재 상태를 보려면 [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) 또는 [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) 카탈로그 뷰를 사용합니다. 데이터베이스가 오프라인 상태일 경우 [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) 카탈로그 뷰에서 파일 상태를 볼 수 있습니다.  
  
 파일 그룹의 파일 상태에 따라 전체 파일 그룹의 사용 가능 여부가 결정됩니다. 파일 그룹을 사용하려면 파일 그룹 내의 모든 파일이 온라인 상태여야 합니다. 파일 그룹의 현재 상태를 보려면 [sys.filegroups](/sql/relational-databases/system-catalog-views/sys-filegroups-transact-sql) 카탈로그 뷰를 사용합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 문으로 오프라인 상태의 파일 그룹에 액세스하려고 하면 오류가 발생하여 실패합니다. 쿼리 최적화 프로그램에서 SELECT 문에 대한 쿼리 계획을 작성할 때 문이 성공하도록 오프라인 파일 그룹에 있는 비클러스터형 인덱스와 인덱싱된 뷰는 사용되지 않습니다. 그러나 오프라인 파일 그룹에 대상 테이블의 힙이나 클러스터형 인덱스가 있는 경우 SELECT 문은 실패합니다. 오프라인 파일 그룹의 인덱스를 사용하여 테이블을 수정하는 INSERT, UPDATE 또는 DELETE 문도 실패합니다.  
  
## <a name="file-state-definitions"></a>파일 상태 정의  
 다음 표에서는 파일 상태를 정의합니다.  
  
|시스템 상태|정의|  
|-----------|----------------|  
|ONLINE|모든 작업에 파일을 사용할 수 있습니다. 데이터베이스가 온라인 상태일 경우 주 파일 그룹의 파일은 항상 온라인 상태입니다. 주 파일 그룹의 파일이 온라인 상태가 아니면 데이터베이스가 온라인 상태가 아니고 보조 파일의 상태가 정의되어 있지 않은 것입니다.|  
|OFFLINE|파일에 액세스할 수 없으며 디스크에 파일이 없을 수도 있습니다. 명시적 사용자 동작으로 인해 파일이 오프라인 상태가 되면 추가 사용자 작업이 수행될 때까지 오프라인 상태로 있습니다.<br /><br /> ** \* 주의 \* \* ** 파일이 손상 되 면 파일을 오프 라인 으로만 설정 해야 합니다. 단, 복원할 수 있습니다. 오프라인으로 설정된 파일을 온라인으로 설정할 수 있는 유일한 방법은 백업에서 파일을 복원하는 것입니다. 단일 파일 복원 방법은 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)를 참조하세요.|  
|RESTORING|파일이 복원되고 있습니다. 페이지 복원이 아닌 전체 파일에 영향을 주는 복원 명령으로 인해 파일이 복원 중 상태가 되어 복원이 완료되고 파일이 복구될 때까지 이 상태로 있습니다.|  
|RECOVERY PENDING|파일 복구가 연기되었습니다. 파일이 복원 및 복구되지 않는 증분 복원 프로세스로 인해 파일이 자동으로 복구 보류 상태가 됩니다. 오류를 해결하고 복구 프로세스를 완료하기 위한 사용자의 추가적인 동작이 필요합니다. 자세한 내용은 [증분 복원 &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md)를 참조 하세요.|  
|SUSPECT|온라인 복원 프로세스 중에 파일 복구가 실패했습니다. 파일이 주 파일 그룹에 속하면 데이터베이스도 주의 대상으로 표시됩니다. 파일이 주 파일 그룹이 아니면 해당 파일만 주의 대상 상태이고 데이터베이스는 계속 온라인 상태입니다.<br /><br /> 다음 방법 중 하나를 사용하여 파일을 사용 가능하게 설정할 때까지 파일이 주의 대상 상태로 있습니다.<br /><br /> 복원 및 복구<br /><br /> DBCC CHECKDB에 REPAIR_ALLOW_DATA_LOSS 사용|  
|DEFUNCT|온라인 상태가 아닐 때 파일이 삭제되었습니다. 오프라인 파일 그룹이 제거되면 파일 그룹의 모든 파일이 존재하지 않음 상태가 됩니다.|  
  
## <a name="related-content"></a>관련 내용  
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [데이터베이스 상태](database-states.md)  
  
 [미러링 상태&#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [데이터베이스 파일 및 파일 그룹](database-files-and-filegroups.md)  
  
  
