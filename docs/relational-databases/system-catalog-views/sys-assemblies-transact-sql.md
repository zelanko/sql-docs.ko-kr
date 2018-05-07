---
title: sys.assemblies (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.assemblies
- assemblies_TSQL
- sys.assemblies_TSQL
- assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assemblies catalog view
ms.assetid: e321753f-293f-42ab-b225-d118713df40b
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 22a200cee9b07332440076feb0981c1610682089
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysassemblies-transact-sql"></a>sys.assemblies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  각 어셈블리에 대해 하나의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|어셈블리의 이름입니다. 데이터베이스 내에서 고유합니다.|  
|**principal_id**|**int**|이 어셈블리를 소유하는 보안 주체의 ID입니다.|  
|**assembly_id**|**int**|어셈블리 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**clr_name**|**nvarchar(4000)**|어셈블리의 단순한 이름, 버전 번호, culture, 공개 키, 아키텍처 등을 인코딩하는 정식 문자열입니다. 이 값은 CLR(공용 언어 런타임) 측에서 어셈블리를 고유하게 식별합니다.|  
|**permission_set**|**tinyint**|어셈블리에 대한 권한 집합/보안 수준입니다.<br /><br /> 1 = 안전한 액세스<br /><br /> 2 = 외부 액세스<br /><br /> 3 = 안전하지 않은 액세스|  
|**permission_set_desc**|**nvarchar(60)**|어셈블리에 대한 권한 집합/보안 수준의 설명입니다.<br /><br /> SAFE_ACCESS<br /><br /> EXTERNAL_ACCESS<br /><br /> UNSAFE_ACCESS|  
|**is_visible**|**bit**|1 = [!INCLUDE[tsql](../../includes/tsql-md.md)] 진입점을 등록할 수 있도록 표시되는 어셈블리입니다.<br /><br /> 0 = 관리되는 호출자 전용 어셈블리입니다. 즉, 이 어셈블리는 데이터베이스의 다른 어셈블리에 내부 구현을 제공합니다.|  
|**create_date**|**datetime**|어셈블리가 작성되거나 등록된 날짜입니다.|  
|**modify_date**|**datetime**|어셈블리가 수정된 날짜입니다.|  
|**is_user_defined**|**bit**|어셈블리의 원본을 나타냅니다.<br /><br /> 0 = 시스템 정의 어셈블리 (Microsoft.SqlServer.Types에 대 한 같은 **hierarchyid** 데이터 형식)<br /><br /> 1 = 사용자 정의 어셈블리|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [CLR 어셈블리 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact SQL&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
