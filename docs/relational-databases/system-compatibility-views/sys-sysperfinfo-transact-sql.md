---
description: sys.sysperfinfo(Transact-SQL)
title: sys.sysperfinfo (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 1122c224e21fa633c2c04cd156a49878fefc7daa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482106"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Windows 시스템 모니터를 통해 표시할 수 있는 내부 성능 카운터의 표현을 포함 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|**Sqlserver: lockmanager** 또는 **Sqlserver: buffermanager**와 같은 성능 개체 이름입니다.|  
|**counter_name**|**nchar(128)**|**페이지 요청** 또는 **요청 된 잠금과**같은 개체 내에 있는 성능 카운터의 이름입니다.|  
|**instance_name**|**nchar(128)**|카운터의 명명된 인스턴스입니다. 예를 들어 각 잠금 유형 (예: **테이블**, **페이지**, **키**등)에 대해 유지 되는 카운터가 있습니다. 유사한 카운터는 인스턴스 이름을 통해 구분합니다.|  
|**cntr_value**|**bigint**|실제 카운터 값입니다. 많은 경우 이는 인스턴스 이벤트의 발생 수를 세는 수준 또는 단순히 수가 증가하는 카운터에 해당합니다.|  
|**cntr_type**|**int**|Windows 성능 아키텍처가 정의한 카운터의 유형입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
