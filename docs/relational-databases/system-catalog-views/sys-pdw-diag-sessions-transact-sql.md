---
description: sys. pdw_diag_sessions (Transact-sql)
title: sys. pdw_diag_sessions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4615bce79c1a748a76a9af02d1991585e4550e12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420027"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>sys. pdw_diag_sessions (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  시스템에 생성 된 다양 한 진단 세션에 대 한 정보를 저장 합니다.  
  
|열 이름|데이터 형식|Description|범위|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|진단 세션의 이름입니다.<br /><br /> 이 보기의 키입니다.||  
|**xml_data**|**nvarchar(4000)**|세션을 설명 하는 XML 페이로드입니다.||  
|**is_active**|**bit**|플래그가 활성 상태 인지 여부를 나타내는 플래그입니다.||  
|**host_address**|**nvarchar(255)**|세션 정의 (컨트롤 노드)를 호스트 하는 컴퓨터의 주소입니다.||  
|**principal_id**|**int**|데이터베이스 수준에서 세션을 만든 사용자의 ID입니다.||  
|**database_id**|**int**|진단 세션의 범위에 해당 하는 데이터베이스의 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
