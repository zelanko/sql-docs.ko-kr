---
title: sys.syslogins (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 41
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b8f420d16d12699825697c47ec1041485d3c43ec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 로그인 계정당 한 개의 행을 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**sid**|**varbinary(85)**|보안 ID입니다.|  
|**상태**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
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
|**sysadmin**|**int**|1 = 로그인이의 멤버는 **sysadmin** 서버 역할입니다.|  
|**securityadmin**|**int**|1 = 로그인이의 멤버는 **securityadmin** 서버 역할입니다.|  
|**serveradmin**|**int**|1 = 로그인이의 멤버는 **serveradmin** 고정된 서버 역할입니다.|  
|**setupadmin**|**int**|1 = 로그인이의 멤버는 **setupadmin** 고정된 서버 역할입니다.|  
|**processadmin**|**int**|1 = 로그인이의 멤버는 **processadmin** 고정된 서버 역할입니다.|  
|**diskadmin**|**int**|1 = 로그인이의 멤버는 **diskadmin** 고정된 서버 역할입니다.|  
|**dbcreator**|**int**|1 = 로그인이의 멤버는 **dbcreator** 고정된 서버 역할입니다.|  
|**bulkadmin**|**int**|1 = 로그인이의 멤버는 **bulkadmin** 고정된 서버 역할입니다.|  
|**loginname**|**nvarchar(128)**|사용자의 로그인 이름입니다. 이전 버전과의 호환성을 위해 제공됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
