---
title: sys.sysconstraints (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysconstraints
- sys.sysconstraints
- sysconstraints_TSQL
- sys.sysconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysconstraints compatibility view
- sysconstraints system table
ms.assetid: f2b2e2ad-ba24-48a1-913c-8ee4e0895dc4
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1f8c58f368afc0ae5a0e0f79f0bdc3717e20e025
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  데이터베이스 내에서 제약 조건을 소유한 개체의 제약 조건 매핑을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|제약 조건 번호입니다.|  
|**id**|**int**|제약 조건을 소유한 테이블의 ID입니다.|  
|**colid**|**smallint**|제약 조건이 정의된 열의 ID입니다.<br /><br /> 0 = 테이블 제약 조건|  
|**spare1**|**tinyint**|예약됨|  
|**상태**|**int**|상태를 나타내는 의사 비트 마스크입니다. 가능한 값은 다음과 같습니다.<br /><br /> 1 = PRIMARY KEY 제약 조건<br /><br /> 2 = UNIQUE KEY 제약 조건<br /><br /> 3 = FOREIGN KEY 제약 조건<br /><br /> 4 = CHECK 제약 조건<br /><br /> 5 = DEFAULT 제약 조건<br /><br /> 16 = 열 수준 제약 조건<br /><br /> 32 = 테이블 수준 제약 조건|  
|**actions**|**int**|예약됨|  
|**error**|**int**|예약됨|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
