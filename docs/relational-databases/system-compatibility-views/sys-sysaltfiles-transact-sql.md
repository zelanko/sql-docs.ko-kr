---
title: sys.sysaltfiles (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysaltfiles_TSQL
- sys.sysaltfiles
- sysaltfiles_TSQL
- sysaltfiles
dev_langs:
- TSQL
helpviewer_keywords:
- sysaltfiles system table
- sys.sysaltfiles compatibility view
ms.assetid: 698dec23-5336-4108-87a5-f8e407f8da09
author: rothja
ms.author: jroth
ms.openlocfilehash: 891e88761cac47be83fb69debbbc5e4cb6c401c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006968"
---
# <a name="syssysaltfiles-transact-sql"></a>sys.sysaltfiles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  특별한 환경에서 사용되며 데이터베이스 내의 각 파일에 해당하는 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|파일의 ID입니다. 각 데이터베이스에 대해 고유합니다.|  
|**groupid**|**smallint**|파일 그룹의 ID입니다.|  
|**size**|**int**|8KB 페이지 단위로 나타낸 파일 크기입니다.|  
|**maxsize**|**int**|8KB 페이지 단위로 나타낸 최대 파일 크기입니다.<br /><br /> 0 = 증가하지 않습니다.<br /><br /> -1 = 디스크가 꽉 찰 때까지 파일이 증가합니다.<br /><br /> 268435456 = 로그 파일이 최대 2TB까지 증가합니다.<br /><br /> 참고: 무제한 로그 파일 크기를 사용 하 여 업그레이드 된 데이터베이스에 로그 파일의 최대 크기에 대 한-1을 보고 합니다.|  
|**growth**|**int**|데이터베이스의 증가 크기입니다.<br /><br /> 0 = 증가하지 않습니다. 상태 값에 따라 페이지의 수 또는 파일 크기의 백분율이 될 수 있습니다. 하는 경우 **상태** 가 0x100000 이면 **증가** 비율로 크기이 고 그렇지 않으면 파일와 페이지 수가 됩니다.|  
|**상태**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**perf**|**int**|예약되어 있습니다.|  
|**dbid**|**smallint**|해당 파일이 속한 데이터베이스의 데이터베이스 ID입니다.|  
|**name**|**sysname**|파일의 논리적 이름입니다.|  
|**filename**|**nvarchar(260)**|물리적 장치의 이름입니다. 여기에는 파일의 전체 경로가 포함됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
