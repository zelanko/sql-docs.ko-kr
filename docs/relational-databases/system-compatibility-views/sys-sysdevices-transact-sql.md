---
title: sys.sysdevices (Transact SQL) | Microsoft Docs
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
- sysdevices
- sysdevices_TSQL
- sys.sysdevices
- sys.sysdevices_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.sysdevices compatibility view
- sysdevices system table
ms.assetid: ac5bcaf4-8fb6-4855-8856-d7643f469361
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b4d25fe28c0489dcfa6f1b892da2d1934cf95cb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="syssysdevices-transact-sql"></a>sys.sysdevices(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 디스크 백업 파일, 테이프 백업 파일 및 데이터베이스 파일에 대한 행을 하나씩 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|백업 파일 또는 데이터베이스 파일의 논리적 이름입니다.|  
|**크기**|**int**|2KB 페이지 단위로 표시한 파일 크기입니다.|  
|**낮은**|**int**|이전 버전과의 호환성을 위해서만 유지됩니다.|  
|**높음**|**int**|이전 버전과의 호환성을 위해서만 유지됩니다.|  
|**상태**|**smallint**|장치 유형을 표시하는 비트맵입니다.<br /><br /> 1 = 기본 디스크<br /><br /> 2 = 물리적 디스크<br /><br /> 4 = 논리적 디스크<br /><br /> 8 = 머리글 건너뛰기<br /><br /> 16 = 백업 파일<br /><br /> 32 = 순차 쓰기<br /><br /> 4096 = 읽기 전용|  
|**cntrltype**|**smallint**|컨트롤러 종류입니다.<br /><br /> 0 = CD-ROM이 아닌 데이터베이스 파일<br /><br /> 2 = 디스크 백업 파일<br /><br /> 3 - 4 = 디스켓 백업 파일<br /><br /> 5 = 테이프 백업 파일<br /><br /> 6 = 명명된 파이프 파일|  
|**phyname**|**nvarchar (260)**|물리적 파일의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40; 시스템 테이블 매핑 Transact SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
