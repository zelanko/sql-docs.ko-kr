---
title: sys. sysremotelogins (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysremotelogins
- sysremotelogins_TSQL
- sys.sysremotelogins
- sys.sysremotelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysremotelogins system table
- sys.sysremotelogins compatibility view
ms.assetid: b7ffcfa6-aed8-41d4-8b70-845439ab813d
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c51ccd657c8a7c5f07bdaf836ba3e279e81c590
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68018127"
---
# <a name="syssysremotelogins-transact-sql"></a>sys.sysremotelogins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인스턴스에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]원격 저장 프로시저를 호출할 수 있는 각 원격 사용자에 대해 하나의 행을 포함 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**remoteserverid**|**smallint**|원격 서버 ID입니다.|  
|**remoteusername**|**sysname**|원격 서버상에서 사용자의 로그인 이름입니다.|  
|**status**|**smallint**|0을 반환합니다.|  
|**sid**|**varbinary(85)**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 보안 ID입니다.|  
|**changedate**|**datetime**|원격 사용자가 추가된 날짜 및 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
