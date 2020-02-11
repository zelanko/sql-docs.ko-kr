---
title: 시스템 호환성 뷰 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compatibility views [SQL Server]
- system tables [SQL Server], compatibility views
- type IDs [SQL Server]
- system views [SQL Server], compatibility
- metadata [SQL Server], views
- backward compatibility [SQL Server], compatibility views
- compatibility [SQL Server], compatibility views
- backward compatibility [SQL Server], system tables
- compatibility [SQL Server], system tables
- user IDs [SQL Server]
ms.assetid: 8e4624f5-9d36-4ce7-9c9e-1fe010fa2122
author: rothja
ms.author: jroth
ms.openlocfilehash: 466dc68da1c5cef56a7debe3953ba38956bb2993
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68018027"
---
# <a name="system-compatibility-views-transact-sql"></a>시스템 호환성 뷰 (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 릴리스에 사용되었던 여러 시스템 테이블이 이제는 뷰 집합으로 구현됩니다. 이러한 뷰를 호환성 뷰라고 하며 이전 버전과의 호환성을 위해서만 제공됩니다. 호환성 뷰는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서 사용되었던 것과 동일한 메타데이터를 노출합니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상에서 새로 추가된 기능과 관련된 메타데이터는 노출하지 않습니다. 따라서 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 또는 분할과 같은 새로운 기능을 사용할 때는 카탈로그 뷰로 전환하여 사용해야 합니다.  
  
 카탈로그 뷰로 업그레이드해야 하는 또 다른 이유는 사용자 ID 및 유형 ID를 저장하는 호환성 뷰 열이 NULL을 반환하거나 산술 오버플로를 트리거할 수 있기 때문입니다. 이것은 사용자, 그룹 및 역할과 데이터 형식을 32,767개 이상 만들 수 있기 때문입니다. 예를 들어 32768 사용자를 만든 후 다음 쿼리를 실행 `SELECT * FROM sys.sysusers`합니다. ARITHABORT를 ON으로 설정하는 경우 산술 오버플로 오류가 발생하여 쿼리가 실패하게 되고 ARITHABORT를 OFF로 설정 하면 **uid** 열이 NULL을 반환 합니다.  
  
 이러한 문제를 피하려면 증가된 사용자 ID 및 유형 ID 수를 처리할 수 있는 새로운 카탈로그 뷰를 사용하는 것이 좋습니다. 다음 표에서는 이 오버플로를 트리거할 수 있는 열을 나열합니다.  
  
|열 이름|호환성 뷰|SQL Server 2005 뷰|  
|-----------------|------------------------|--------------------------|  
|**xusertype**|**syscolumns**|**sys.columns**|  
|**usertype**|**syscolumns**|**sys.columns**|  
|**memberuid**|**sysmembers**|**sys.database_role_members**|  
|**groupuid**|**sysmembers**|**sys.database_role_members**|  
|**uid**|**sysobjects**|**sys.objects**|  
|**uid**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**grantor**|**sysprotects**|**sys.database_permissions**<br /><br /> **sys.server_permissions**|  
|**xusertype**|**systypes**|**sys.types**|  
|**uid**|**systypes**|**sys.types**|  
|**uid**|**sysusers**|**sys.database_principals**|  
|**altuid**|**sysusers**|**sys.database_principals**|  
|**gid**|**sysusers**|**sys.database_principals**|  
|**uid**|**syscacheobjects**|**sys.dm_exec_plan_attributes**|  
|**uid**|**sysprocesses**|**sys.dm_exec_requests**|  
  
 사용자 데이터베이스에서 참조 되는 경우 SQL Server 2000 (예: **sys.syslanguages** 또는 **syscacheobjects**)에서 더 이상 사용 되지 않는 것으로 발표 된 시스템 테이블은 이제 **sys** 스키마의 이전 버전과의 호환성 뷰에 바인딩됩니다. SQL Server 2000 시스템 테이블이 여러 버전에서 더 이상 사용되지 않으므로 이는 새로운 변경 사항이 아닙니다.  
  
 예: 사용자가 사용자 데이터베이스에서 **sys.syslanguages** 라는 사용자 테이블을 만드는 경우 SQL Server 2008에서 해당 데이터베이스의 문은 `SELECT * from dbo.syslanguages;` 사용자 테이블의 값을 반환 합니다. SQL Server 2012부터이 연습에서는 시스템 뷰 **sys.syslanguages**의 데이터를 반환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
