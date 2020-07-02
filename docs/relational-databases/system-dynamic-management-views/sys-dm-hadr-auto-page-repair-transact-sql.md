---
title: sys. dm_hadr_auto_page_repair (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 02/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 53e41822c48bb61e9253ddd22eb1f348d539ca7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752856"
---
# <a name="sysdm_hadr_auto_page_repair-transact-sql"></a>sys.dm_hadr_auto_page_repair(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  서버 인스턴스가 모든 가용성 그룹에 대해 호스팅하는 가용성 복제본의 모든 가용성 데이터베이스에 대해 수행하는 자동 페이지 복구 시도당 한 개의 행을 반환합니다. 이 뷰에는 지정된 주 데이터베이스 또는 보조 데이터베이스의 최신 자동 페이지 복구 시도에 대한 행이 포함됩니다(데이터베이스당 최대 100개 행). 데이터베이스가 최대값에 도달하는 즉시 다음 자동 페이지 복구 시도에 대한 행이 기존 항목 중 하나를 대체합니다.
  
  다음 표에서는 다양 한 열의 의미를 정의 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|이 행이 해당하는 데이터베이스의 ID입니다.|  
|**file_id**|**int**|해당 페이지가 있는 파일의 ID입니다.|  
|**page_id**|**bigint**|파일에 있는 페이지의 ID입니다.|  
|**error_type**|**int**|오류 유형입니다. 값은 다음이 될 수 있습니다.<br /><br /> **-** 1 = 모든 하드웨어 823 오류<br /><br /> 1 = 잘못된 체크섬 또는 조각난 페이지 이외의 824 오류(예: 잘못된 페이지 ID)<br /><br /> 2 = 잘못된 체크섬<br /><br /> 3 = 조각난 페이지|  
|**page_status**|**int**|페이지 복구 시도의 상태입니다.<br /><br /> 2 = 파트너의 요청에 대해 대기 중입니다.<br /><br /> 3 = 파트너에게 요청이 전송되었습니다.<br /><br /> 4 = 페이지를 성공적으로 복구 했습니다.<br /><br /> 5 = 마지막 시도/자동 페이지 복구가 페이지 복구를 다시 시도 하는 동안 페이지를 복구할 수 없습니다.|  
|**modification_time**|**datetime**|페이지 상태가 마지막으로 변경된 시간입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [자동 페이지 복구 &#40;가용성 그룹: 데이터베이스 미러링&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Transact-sql&#41;suspect_pages &#40;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

