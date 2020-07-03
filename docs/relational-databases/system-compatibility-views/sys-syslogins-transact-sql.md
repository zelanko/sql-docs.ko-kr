---
title: sys.sys로그인 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslogins_TSQL
- syslogins
- sys.syslogins
- sys.syslogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syslogins compatibility view
- syslogins system table
ms.assetid: 4cb34f17-a4bb-469f-a218-71f074e6308f
author: rothja
ms.author: jroth
ms.openlocfilehash: eb1fd5b8dcf9867cb61452534a742cc929a41396
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891944"
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 로그인 계정당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**sid**|**varbinary(85)**|보안 ID입니다.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|로그인이 추가된 날짜입니다.|  
|**updatedate**|**datetime**|로그인이 업데이트된 날짜입니다.|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**timelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|사용자의 로그인 이름입니다.|  
|**dbname**|**sysname**|연결 시 사용자의 기본 데이터베이스 이름입니다.|  
|**password**|**nvarchar(128)**|NULL을 반환합니다.|  
|**language**|**sysname**|사용자의 기본 언어입니다.|  
|**denylogin**|**int**|1 = 로그인이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 또는 그룹이며 액세스가 거부되었습니다.|  
|**hasaccess**|**int**|1 = 로그인에 대한 서버 액세스가 허용되었습니다.|  
|**isntname**|**int**|1 = 로그인이 Windows 사용자 또는 그룹입니다.<br /><br /> 0 = 로그인이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인입니다.|  
|**isntgroup**|**int**|1 = 로그인이 Windows 그룹입니다.|  
|**isntuser**|**int**|1 = 로그인이 Windows 사용자입니다.|  
|**sysadmin**|**int**|1 = 로그인이 **sysadmin** 서버 역할의 멤버입니다.|  
|**securityadmin**|**int**|1 = 로그인이 **securityadmin** 서버 역할의 멤버입니다.|  
|**serveradmin**|**int**|1 = 로그인이 **serveradmin** 고정 서버 역할의 멤버입니다.|  
|**setupadmin**|**int**|1 = 로그인이 **setupadmin** 고정 서버 역할의 멤버입니다.|  
|**processadmin**|**int**|1 = 로그인이 **processadmin** 고정 서버 역할의 멤버입니다.|  
|**diskadmin**|**int**|1 = 로그인이 **diskadmin** 고정 서버 역할의 멤버입니다.|  
|**dbcreator**|**int**|1 = 로그인이 **dbcreator** 고정 서버 역할의 멤버입니다.|  
|**bulkadmin**|**int**|1 = 로그인이 **bulkadmin** 고정 서버 역할의 멤버입니다.|  
|**loginname**|**nvarchar(128)**|사용자의 로그인 이름입니다. 이전 버전과의 호환성을 위해 제공됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
