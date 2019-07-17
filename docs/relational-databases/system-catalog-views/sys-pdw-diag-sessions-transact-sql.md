---
title: sys.pdw_diag_sessions (TRANSACT-SQL) | Microsoft Docs
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
ms.openlocfilehash: fa06005679e31381f723b30b9f68e5ce0d89ae1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127688"
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  시스템에서 생성 된 다양 한 진단 세션에 대 한 정보를 보유 합니다.  
  
|열 이름|데이터 형식|설명|범위|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|진단 세션의 이름입니다.<br /><br /> 이 보기에 대 한 키입니다.||  
|**xml_data**|**nvarchar(4000)**|세션을 설명 하는 XML 페이로드입니다.||  
|**is_active**|**bit**|플래그를 활성 상태 인지 여부를 나타내는 플래그입니다.||  
|**host_address**|**nvarchar(255)**|해당 세션 정의가 (제어 노드)를 호스트 하는 컴퓨터의 주소입니다.||  
|**principal_id**|**int**|데이터베이스 수준에서 세션을 만든 사용자의 ID입니다.||  
|**database_id**|**int**|진단 세션의 범위에 있는 데이터베이스의 ID입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
