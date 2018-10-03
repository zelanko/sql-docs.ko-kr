---
title: sys.assemblies (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 335b536d3356f5bfefa6cf5efd71b34327c79708
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740901"
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
|**is_user_defined**|**bit**|어셈블리의 원본을 나타냅니다.<br /><br /> 0 = 시스템 정의 어셈블리 (같은 경우 Microsoft.SqlServer.Types 합니다 **hierarchyid** 데이터 형식)<br /><br /> 1 = 사용자 정의 어셈블리|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 어셈블리 카탈로그 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;TRANSACT-SQL&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
