---
title: sys. pdw_health_alerts (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2e3ab735a19342e1ecc1a941a185832edae61262
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627447"
---
# <a name="syspdw_health_alerts-transact-sql"></a>sys. pdw_health_alerts (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  시스템에서 발생할 수 있는 다양 한 경고에 대 한 속성을 저장 합니다. 이는 경고에 대 한 카탈로그 테이블입니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|경고의 고유 식별자입니다.<br /><br /> 이 보기의 키입니다.|NOT NULL|  
|component_id|**int**|이 경고가 적용 되는 구성 요소의 ID입니다. 구성 요소는 "전원 공급 장치"와 같은 일반적인 구성 요소 식별자 이며 설치에 한정 되지 않습니다. [Pdw_health_components &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)을 참조 하십시오.|NOT NULL|  
|alert_name|**nvarchar(255)**|경고의 이름입니다.|NOT NULL|  
|state|**nvarchar(32)**|경고의 상태입니다.|NOT NULL<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> 주기와<br /><br /> 'NonOperational'<br /><br /> 성능<br /><br /> 오류가|  
|severity|**nvarchar(32)**|경고의 심각도입니다.|NOT NULL<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> 위해서<br /><br /> 내용의<br /><br /> 메시지가|  
|type|**nvarchar(32)**|경고의 유형입니다.|NOT NULL<br /><br /> 가능한 값은 다음과 같습니다.<br /><br /> StatusChange-장치 상태가 변경 되었습니다.<br /><br /> Threshold-값이 임계값을 초과 했습니다.|  
|description|**nvarchar(4000)**|경고에 대한 설명입니다.|NOT NULL|  
|condition(조건)|**nvarchar(255)**|Type = Threshold 인 경우 사용 됩니다. 경고 임계값을 계산 하는 방법을 정의 합니다.|NULL|  
|상태|**nvarchar(32)**|경고 상태|NULL|  
|condition_value|**bit**|시스템 작업 중에 경고가 발생할 수 있는지 여부를 나타냅니다.|NULL<br /><br /> 가능한 값<br /><br /> 0-경고가 생성 되지 않습니다.<br /><br /> 1-경고가 생성 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
