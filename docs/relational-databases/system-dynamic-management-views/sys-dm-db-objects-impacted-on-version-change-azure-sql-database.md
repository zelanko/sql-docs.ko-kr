---
title: sys. dm_db_objects_impacted_on_version_change
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 0255f7260044ee5c09d020f3ba6310d24bc8cb74
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843859"
---
# <a name="sysdm_db_objects_impacted_on_version_change-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  이 데이터베이스 범위 시스템 뷰는 조기 경보 시스템으로 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 주요 릴리스 업그레이드에 의해 영향을 받는 개체를 확인할 수 있도록 설계되어 있습니다. 업그레이드 전후에 이 뷰를 사용하여 영향을 받는 개체의 전체 목록을 가져올 수 있습니다. 전체 서버에서 전체 개수를 가져오려면 각 데이터베이스에서 이 뷰를 쿼리해야 합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|class|**int** NULL이 아님|영향을 받는 개체의 클래스:<br /><br /> **1** = 제약 조건<br /><br /> **7** = 인덱스 및 힙|  
|class_desc|**nvarchar (60)** NULL이 아님|클래스 설명:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int** NULL이 아님|제약 조건의 개체 ID 또는 인덱스나 힙을 포함하는 테이블의 개체 ID입니다.|  
|minor_id|**int** N|제약 조건의 경우 **NULL**<br /><br /> 인덱스 및 힙의 경우 Index_id|  
|dependency|**nvarchar (60)** NULL이 아님|제약 조건 또는 인덱스에게 영향을 미치는 종속성에 대한 설명입니다. 업그레이드 시 생성되는 경고에 대해서도 동일한 값이 사용됩니다.<br /><br /> 예:<br /><br /> **space** (내장 함수)<br /><br /> **geometry** (시스템 UDT의 경우)<br /><br /> **geography::P arse** (시스템 UDT 메서드의 경우)|  
  
## <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **sys. dm_db_objects_impacted_on_version_change** 에 대 한 쿼리를 보여 줍니다. 다음 주 서버 버전으로 업그레이드 하 여 영향을 받는 개체를 찾을 수 있습니다.  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>주의  
  
### <a name="how-to-update-impacted-objects"></a>영향을 받는 개체를 업데이트하는 방법  
 다음 순서 단계는 곧 있을 6월 서비스 릴리스 업그레이드 이후에 수행될 수정 작업에 대해 설명합니다.  
  
|주문|영향을 받는 개체|수정 동작|  
|-----------|---------------------|-----------------------|  
|1\.|**인덱스**|Dm_db_objects_impacted_on_version_change으로 식별 되는 인덱스를 다시 작성 **합니다** (예: `ALTER INDEX ALL ON <table> REBUILD`<br />또는<br />`ALTER TABLE <table> REBUILD`|  
|2|**개체**|기 하 도형 및 기본 테이블의 지리 데이터가 다시 계산 된 후에는 **dm_db_objects_impacted_on_version_change** 으로 식별 되는 모든 제약 조건이 유효성을 다시 검사 해야 합니다. ALTER TABLE을 사용하여 제약 조건의 유효성을 다시 검증합니다. <br />예를 들어 <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />또는<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
