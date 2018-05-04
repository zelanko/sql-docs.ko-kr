---
title: sysmergepartitioninfo (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergepartitioninfo_TSQL
- sysmergepartitioninfo
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfo system table
ms.assetid: 7429ad2c-dd33-4f7d-89cc-700e083af518
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bcf556a371dc391b41e08778434b25131bfcf09e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmergepartitioninfo-transact-sql"></a>sysmergepartitioninfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 아티클의 파티션에 대한 정보를 제공합니다. 로컬 데이터베이스에 정의된 각 병합 아티클에 대해 한 행을 포함합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**uniqueidentifier**|지정된 아티클의 고유한 ID입니다.|  
|**pubid**|**uniqueidentifier**|이 게시의 고유한 ID이며 게시가 추가될 때 생성됩니다.|  
|**partition_view_id**|**int**|이 테이블에 대한 파티션 뷰의 ID입니다. 이 뷰는 아티클의 각 행과 아티클이 속해 있는 다른 파티션 ID 사이의 매핑을 보여 줍니다.|  
|**repl_view_id**|**int**|추가될 예정입니다.|  
|**partition_deleted_view_rule**|**nvarchar(4000)**|이전의 열 값을 기준으로 삭제 또는 업데이트된 각 행의 파티션 ID를 검색하기 위해 병합 복제 트리거 내에서 사용하는 SQL 문입니다.|  
|**partition_inserted_view_rule**|**nvarchar(4000)**|새로운 열 값을 기준으로 삽입 또는 업데이트된 각 행의 파티션 ID를 검색하기 위해 병합 복제 트리거 내에서 사용하는 SQL 문입니다.|  
|**membership_eval_proc_name**|**sysname**|에 있는 행의 한 현재 파티션 Id를 평가 하는 프로시저의 이름 **MSmerge_contents**합니다.|  
|**column_list**|**nvarchar(4000)**|아티클에 복제된 열을 쉼표로 구분한 목록입니다.|  
|**column_list_blob**|**nvarchar(4000)**|BLOB(Binary Large Object) 열을 포함하여 아티클에 복제된 열을 쉼표로 구분한 목록입니다.|  
|**expand_proc**|**sysname**|새로 삽입된 부모 행의 모든 자식 행, 파티션이 변경된 부모 행 및 삭제된 부모 행에 대한 파티션 ID를 다시 평가하는 프로시저의 이름입니다.|  
|**logical_record_parent_nickname**|**int**|논리적 레코드에서 지정된 아티클에 대한 최상위 부모의 애칭입니다.|  
|**logical_record_view**|**int**|각 자식 rowguid에 해당하는 최상위 부모 아티클의 rowguid를 출력하는 뷰입니다.|  
|**logical_record_deleted_view_rule**|**nvarchar(4000)**|비슷한 **logical_record_view**"삭제 된" 테이블에 있는 자식 행 업데이트 및 삭제 트리거에서 표시 한다는 점을 제외 하 고, 합니다.|  
|**logical_record_level_conflict_detection**|**bit**|충돌을 논리적 레코드 수준에서 감지할지 또는 행이나 열 수준에서 감지할지 여부를 나타냅니다.<br /><br /> **0** = 행 또는 열 수준 충돌 감지가 사용 됩니다.<br /><br /> **1** = 논리적 레코드 충돌 감지가 사용 하는 경우 구독자에서 레코드 충돌로 처리는 게시자에서 행의 변경 및 별도의 변경 행이 같은 논리를 합니다.<br /><br /> 이 값이 **1**, 논리적 레코드 수준의 충돌 해결만을 사용할 수 있습니다.|  
|**logical_record_level_conflict_resolution**|**bit**|충돌을 논리적 레코드 수준에서 해결할지 또는 행이나 열 수준에서 해결할지 여부를 나타냅니다.<br /><br /> **0** = 행 또는 열 수준 해결이 사용 됩니다.<br /><br /> **1** =는 충돌 시 적용 되에서 전체 논리적 레코드는 무시 되 면에 전체 논리적 레코드를 덮어씁니다.<br /><br /> 값이 **1** 모두 논리적 레코드 수준의 감지 및 행 또는 열 수준 감지에는 사용할 수 있습니다.|  
|**partition_options**|**tinyint**|아티클의 데이터 분할 방식을 정의합니다. 데이터를 분할하면 모든 행이 하나의 파티션 또는 하나의 구독에만 속한 경우 성능을 최적화할 수 있습니다. *partition_options* 다음 값 중 하나일 수 있습니다.<br /><br /> **0** = 필터링 문서가 정적 이거나 각 파티션에, 즉 "겹치는" 파티션에 대 한 데이터의 고유 하위 집합을 생성 하지 않습니다.<br /><br /> **1** = 파티션이 겹치며 구독자에서 DML 업데이트 행이 속한 파티션을 변경할 수 없습니다.<br /><br /> **2** = 필터링 하면 문서에는 겹치지 않는 파티션이 생성 되지만 여러 구독자가 동일한 파티션을 받을 수 있습니다.<br /><br /> **3** = 필터링 하면 문서에는 각 구독에 대해 고유한 겹치지 않는 파티션이 생성 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
