---
title: sys.dm_hadr_auto_page_repair (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72750c250e45c6a3fba647ae212b0a5b63a11abc
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  서버 인스턴스가 모든 가용성 그룹에 대해 호스팅하는 가용성 복제본의 모든 가용성 데이터베이스에 대해 수행하는 자동 페이지 복구 시도당 한 개의 행을 반환합니다. 이 뷰에는 지정된 주 데이터베이스 또는 보조 데이터베이스의 최신 자동 페이지 복구 시도에 대한 행이 포함됩니다(데이터베이스당 최대 100개 행). 데이터베이스가 최대값에 도달하는 즉시 다음 자동 페이지 복구 시도에 대한 행이 기존 항목 중 하나를 대체합니다.
  
  다음 표에서 다양 한 열의 의미를 정의합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|이 행이 해당하는 데이터베이스의 ID입니다.|  
|**file_id**|**int**|해당 페이지가 있는 파일의 ID입니다.|  
|**page_id**|**bigint**|파일에 있는 페이지의 ID입니다.|  
|**error_type**|**int**|오류 유형입니다. 값은 다음이 될 수 있습니다.<br /><br /> **-**1 = 모든 하드웨어 823 오류<br /><br /> 1 = 824 잘못 된 체크섬 이나 조각난된 페이지 (예: 잘못 된 페이지 ID) 이외의 다른 오류<br /><br /> 2 = 잘못된 체크섬<br /><br /> 3 = 조각난 페이지|  
|**page_status**|**int**|페이지 복구 시도의 상태입니다.<br /><br /> 2 = 파트너의 요청에 대해 대기 중입니다.<br /><br /> 3 = 파트너에게 요청이 전송되었습니다.<br /><br /> 4 = 자동 페이지 복구를 위해 대기 중입니다(파트너로부터 응답을 수신함).<br /><br /> 5 = 자동 페이지 복구가 성공적으로 수행되었으며 해당 페이지를 사용할 수 있습니다.<br /><br /> 6 = 복구할 수 없습니다. 이는 페이지 복구 시도 중 오류가 발생했음을 나타냅니다. 예를 들어 파트너에서도 페이지가 손상되었거나 파트너와의 연결이 끊어졌거나 네트워크 문제가 발생한 경우입니다. 페이지에서 다시 손상이 발생할 경우 파트너가 다시 해당 페이지를 요청하므로 이 상태가 최종 상태는 아닙니다.|  
|**modification_time**|**datetime**|페이지 상태가 마지막으로 변경된 시간입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [자동 페이지 복구&#40;가용성 그룹: 데이터베이스 미러링&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages&#40; Transact SQL &#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

