---
title: sys.pdw_health_alerts (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6f8281d520f64580af8432dbf2004227ce628d41
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987195"
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  시스템에서 발생할 수 있는 다양 한 경고에 대 한 속성을 저장 합니다. 이 경고에 대 한 카탈로그 테이블입니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|경고의 고유 식별자입니다.<br /><br /> 이 보기에 대 한 키입니다.|NOT NULL|  
|component_id|**int**|이 경고 구성 요소의 ID에 적용 됩니다. 구성 요소는 "전원 공급 장치를"와 같은 일반적인 구성 요소 식별자 및 설치에 한정 되지 않습니다. 참조 [sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)합니다.|NOT NULL|  
|alert_name|**nvarchar(255)**|경고의 이름입니다.|NOT NULL|  
|state|**nvarchar(32)**|경고의 상태입니다.|NOT NULL<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> ' Operational'<br /><br /> 'NonOperational'<br /><br /> ' 성능이 저하 '<br /><br /> ' 실패 '|  
|severity|**nvarchar(32)**|경고의 심각도입니다.|NOT NULL<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> ' 정보 '<br /><br /> ' 경고 '<br /><br /> ' Error'|  
|유형|**nvarchar(32)**|경고의 형식입니다.|NOT NULL<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> StatusChange-장치 상태 변경 되었습니다.<br /><br /> 임계값-값이 임계값을 초과 했습니다.|  
|description|**nvarchar(4000)**|경고 설명입니다.|NOT NULL|  
|condition(조건)|**nvarchar(255)**|경우에 사용 되는 입력 임계값 =. 경고 임계값을 계산 하는 방법을 정의 합니다.|NULL|  
|상태|**nvarchar(32)**|경고 상태|NULL|  
|condition_value|**bit**|경고는 시스템 작업 중에 발생할 수 있는지 여부를 나타냅니다.|NULL<br /><br /> 가능한 값<br /><br /> 0-경고가 생성 되지 않습니다.<br /><br /> 1-경고가 생성 됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
