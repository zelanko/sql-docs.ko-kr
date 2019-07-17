---
title: sys.sysperfinfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
ms.openlocfilehash: e6ce86e7be7d54e95c2336691b53ea12ff0d8575
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076502"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  포함 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Windows 시스템 모니터를 통해 표시 될 수 있는 내부 성능 카운터의 표현입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|성능 개체 이름와 같은 **SQLServer:LockManager** 하거나 **SQLServer:BufferManager**합니다.|  
|**counter_name**|**nchar(128)**|개체 내의 성능 카운터의 이름을 같은 **페이지 요청** 하거나 **Locks Requested**합니다.|  
|**instance_name**|**nchar(128)**|카운터의 명명된 인스턴스입니다. 예를 들어,와 같은 각 유형의 잠금에 대 한 유지 관리 하는 카운터가 있습니다. **테이블**, **페이지**하십시오 **키**등. 유사한 카운터는 인스턴스 이름을 통해 구분합니다.|  
|**cntr_value**|**bigint**|실제 카운터 값입니다. 많은 경우 이는 인스턴스 이벤트의 발생 수를 세는 수준 또는 단순히 수가 증가하는 카운터에 해당합니다.|  
|**cntr_type**|**int**|Windows 성능 아키텍처가 정의한 카운터의 유형입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
