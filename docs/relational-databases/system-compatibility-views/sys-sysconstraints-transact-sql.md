---
description: sys.sysconstraints(Transact-SQL)
title: sys.sys제약 조건 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a50f67470a91af617ae76baadf1a029bfa56b59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423337"
---
# <a name="syssysconstraints-transact-sql"></a>sys.sysconstraints(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 내에서 제약 조건을 소유한 개체의 제약 조건 매핑을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|제약 조건 번호입니다.|  
|**id**|**int**|제약 조건을 소유한 테이블의 ID입니다.|  
|**id**|**smallint**|제약 조건이 정의된 열의 ID입니다.<br /><br /> 0 = 테이블 제약 조건|  
|**spare1**|**tinyint**|예약됨|  
|**status**|**int**|상태를 나타내는 의사 비트 마스크입니다. 가능한 값은 다음과 같습니다.<br /><br /> 1 = PRIMARY KEY 제약 조건<br /><br /> 2 = UNIQUE KEY 제약 조건<br /><br /> 3 = FOREIGN KEY 제약 조건<br /><br /> 4 = CHECK 제약 조건<br /><br /> 5 = DEFAULT 제약 조건<br /><br /> 16 = 열 수준 제약 조건<br /><br /> 32 = 테이블 수준 제약 조건|  
|**actions**|**int**|예약됨|  
|**error**|**int**|예약됨|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
