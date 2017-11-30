---
title: sys.sysfiles (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7190a2389fc1504cb8068eb5ea9b6ffd7ed127fb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스에 있는 각 파일당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|각 데이터베이스에 대해 고유한 파일 ID입니다.|  
|**그룹 id**|**smallint**|파일 그룹의 ID입니다.|  
|**크기**|**int**|8KB 페이지 단위로 나타낸 파일의 크기입니다.|  
|**maxsize**|**int**|8KB 페이지 단위로 나타낸 최대 파일 크기입니다.<br /><br /> 0 = 증가하지 않습니다.<br /><br /> -1 = 디스크가 꽉 찰 때까지 파일이 증가합니다.<br /><br /> 268435456 = 로그 파일이 최대 2TB까지 증가합니다.<br /><br /> 참고: 무제한 로그 파일 크기와 업그레이드 된 데이터베이스에 로그 파일의 최대 크기에 대 한-1을 보고 합니다.|  
|**증가**|**int**|데이터베이스의 증가 크기입니다. 페이지의 수 또는 값에 따라 파일 크기의 백분율이 될 수 있습니다 **상태**합니다.<br /><br /> 0 = 증가하지 않습니다.|  
|**상태**|**int**|에 대 한 상태 비트는 **증가** 값 (mb) 또는 크기 (KB)입니다.<br /><br /> 0x2 = 디스크 파일<br /><br /> 0x40 = 로그 파일<br /><br /> 0x100000 = 증가율 이 값은 백분율이며 페이지 수가 아닙니다.|  
|**성능**|**int**|예약되어 있습니다.|  
|**name**|**sysname**|파일의 논리적 이름입니다.|  
|**파일 이름**|**nvarchar (260)**|물리적 장치의 이름입니다. 여기에는 파일의 전체 경로가 포함됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40; 시스템 테이블 매핑 Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
