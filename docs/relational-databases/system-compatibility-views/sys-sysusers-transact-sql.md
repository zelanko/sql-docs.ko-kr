---
title: sys.sysusers (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysusers
- sys.sysusers_TSQL
- sysusers_TSQL
- sysusers
dev_langs:
- TSQL
helpviewer_keywords:
- sysusers system table
- sys.sysusers compatibility view
ms.assetid: 5f0e6a8d-c983-44f6-97e9-aab5bff67d18
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d5cdf3c9a8f78e3b2035fdac345940536fd2275b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssysusers-transact-sql"></a>sys.sysusers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  각각에 대해 하나의 행을 포함 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자, Windows 그룹, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자, 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할에에서 지정 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**uid**|**smallint**|해당 데이터베이스에서 고유한 사용자 ID입니다.<br /><br /> 1 = 데이터베이스 소유자<br /><br /> 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.|  
|**상태**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|해당 데이터베이스에서 고유한 사용자 이름 또는 그룹 이름입니다.|  
|**sid**|**varbinary(85)**|해당 항목에 대한 SID(보안 ID)입니다.|  
|**역할**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|계정이 추가된 날짜입니다.|  
|**updatedate**|**datetime**|계정을 마지막으로 변경한 날짜입니다.|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> 사용자 및 역할 수가 32,767을 초과하는 경우 오버플로되거나 NULL을 반환합니다.|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**smallint**|해당 사용자가 속한 그룹의 ID입니다. 경우 **uid** 동일 **gid**,이 항목 그룹을 정의 합니다. 그룹과 사용자를 합한 수가 32,767을 초과하면 오버플로되거나 NULL을 반환합니다.|  
|**environ**|**varchar(255)**|예약되어 있습니다.|  
|**hasdbaccess**|**int**|1 = 계정에 데이터베이스 액세스가 있습니다.|  
|**islogin**|**int**|1 = 계정이 로그인 계정이 있는 Windows 그룹, Windows 사용자 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자입니다.|  
|**isntname**|**int**|1 = 계정이 Windows 사용자 또는 Windows 그룹입니다.|  
|**isntgroup**|**int**|1 = 계정이 Windows 그룹입니다.|  
|**isntuser**|**int**|1 = 계정이 Windows 사용자입니다.|  
|**issqluser**|**int**|1 = 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자입니다.|  
|**isaliased**|**int**|1 = 계정이 다른 사용자의 별칭입니다.|  
|**issqlrole**|**int**|1 = 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할입니다.|  
|**isapprole**|**int**|1 = 계정이 응용 프로그램 역할입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
