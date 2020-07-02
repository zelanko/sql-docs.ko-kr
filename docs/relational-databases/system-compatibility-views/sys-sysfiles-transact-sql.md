---
title: sys.sys파일 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
author: rothja
ms.author: jroth
ms.openlocfilehash: 23f0a88653887177a84da079d00550dc9915f0d2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786390"
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스에 있는 각 파일당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|각 데이터베이스에 대해 고유한 파일 ID입니다.|  
|**groupid**|**smallint**|파일 그룹의 ID입니다.|  
|**size**|**int**|8KB 페이지 단위로 나타낸 파일의 크기입니다.|  
|**크기**|**int**|8KB 페이지 단위로 나타낸 최대 파일 크기입니다.<br /><br /> 0 = 증가하지 않습니다.<br /><br /> -1 = 디스크가 꽉 찰 때까지 파일이 증가합니다.<br /><br /> 268435456 = 로그 파일이 최대 2TB까지 증가합니다.<br /><br /> 참고: 무제한 로그 파일 크기로 업그레이드 된 데이터베이스는 로그 파일의 최대 크기에 대해-1을 보고 합니다.|  
|**growth**|**int**|데이터베이스의 증가 크기입니다. **상태**값에 따라 페이지의 수 또는 파일 크기의 백분율이 될 수 있습니다.<br /><br /> 0 = 증가하지 않습니다.|  
|**status**|**int**|메가바이트 (MB) 또는 킬로바이트 (KB)의 **증가** 값에 대 한 상태 비트입니다.<br /><br /> 0x2 = 디스크 파일<br /><br /> 0x40 = 로그 파일<br /><br /> 0x100000 = 증가율 이 값은 백분율이며 페이지 수가 아닙니다.|  
|**성능**|**int**|예약되어 있습니다.|  
|**name**|**sysname**|파일의 논리적 이름입니다.|  
|**filename**|**nvarchar(260)**|물리적 디바이스의 이름입니다. 여기에는 파일의 전체 경로가 포함됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
