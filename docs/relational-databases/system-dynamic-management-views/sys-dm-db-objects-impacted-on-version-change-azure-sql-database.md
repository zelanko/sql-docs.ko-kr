---
title: sys.dm_db_objects_impacted_on_version_change (Azure SQL Database) | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: b6f6538aa13b2236c7dca52189b37addad85ae53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62507264"
---
# <a name="sysdmdbobjectsimpactedonversionchange-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  이 데이터베이스 범위 시스템 뷰는 조기 경보 시스템으로 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 주요 릴리스 업그레이드에 의해 영향을 받는 개체를 확인할 수 있도록 설계되어 있습니다. 업그레이드 전후에 이 뷰를 사용하여 영향을 받는 개체의 전체 목록을 가져올 수 있습니다. 전체 서버에서 전체 개수를 가져오려면 각 데이터베이스에서 이 뷰를 쿼리해야 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|class|**int** NOT NULL|영향을 받는 개체의 클래스:<br /><br /> **1** = constraint<br /><br /> **7** = 인덱스 및 힙|  
|class_desc|**nvarchar(60)** NOT NULL|클래스 설명:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int** NOT NULL|제약 조건의 개체 ID 또는 인덱스나 힙을 포함하는 테이블의 개체 ID입니다.|  
|minor_id|**int** NULL|**NULL** 제약 조건에 대 한<br /><br /> 인덱스 및 힙의 경우 Index_id|  
|dependency|**nvarchar(60)** NOT NULL|제약 조건 또는 인덱스에게 영향을 미치는 종속성에 대한 설명입니다. 업그레이드 시 생성되는 경고에 대해서도 동일한 값이 사용됩니다.<br /><br /> 예를 들면 다음과 같습니다.<br /><br /> **공간** (에 대 한 내장 함수)<br /><br /> **기 하 도형** (시스템용: UDT)<br /><br /> **geography:: parse** (시스템 UDT 메서드의 경우)에 대 한|  
  
## <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서 쿼리를 보여 줍니다 **sys.dm_db_objects_impacted_on_version_change** 다음 주요 서버 버전 업그레이드에 영향을 받는 개체를 찾으려면  
  
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
  
## <a name="remarks"></a>Remarks  
  
### <a name="how-to-update-impacted-objects"></a>영향을 받는 개체를 업데이트하는 방법  
 다음 순서 단계는 곧 있을 6월 서비스 릴리스 업그레이드 이후에 수행될 수정 작업에 대해 설명합니다.  
  
|주문|영향을 받는 개체|수정 동작|  
|-----------|---------------------|-----------------------|  
|1|**인덱스**|로 식별 되는 모든 인덱스 다시 작성 **sys.dm_db_objects_impacted_on_version_change** 예를 들어:  `ALTER INDEX ALL ON <table> REBUILD`<br />로 구분하거나 여러<br />`ALTER TABLE <table> REBUILD`|  
|2|**개체**|로 식별 되는 모든 제약 조건을 **sys.dm_db_objects_impacted_on_version_change** 기본 테이블에 geometry 및 geography 데이터 다시 계산 되 면 유효성을 재검사 해야 합니다. ALTER TABLE을 사용하여 제약 조건의 유효성을 다시 검증합니다. <br />이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />로 구분하거나 여러<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
