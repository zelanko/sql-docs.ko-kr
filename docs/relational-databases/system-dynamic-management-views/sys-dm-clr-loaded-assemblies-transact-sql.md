---
title: sys. dm_clr_loaded_assemblies (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1cd677e516048aa52badec7fc9875e5a5b13f25a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138663"
---
# <a name="sysdm_clr_loaded_assemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 주소 공간으로 로드되는 각각의 관리되는 사용자 어셈블리에 대해 행을 반환합니다. 이 뷰를 사용 하 여에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]실행 중인 CLR 통합 관리 되는 데이터베이스 개체를 이해 하 고 문제를 해결할 수 있습니다.  
  
 어셈블리는 관리되는 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 정의 및 배포하는 데 사용되는 관리 코드 DLL 파일입니다. 사용자가 이러한 관리되는 데이터베이스 개체 중 하나를 실행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 CLR은 관리되는 데이터베이스 개체가 정의되는 어셈블리 및 해당 참조를 로드합니다. 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드된 상태로 유지되어 성능을 향상시키므로 어셈블리에 포함된 관리되는 데이터베이스 개체가 어셈블리를 다시 로드하지 않고 나중에 호출될 수 있습니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메모리가 부족해질 때까지 어셈블리가 언로드되지 않습니다. 어셈블리 및 CLR 통합에 대 한 자세한 내용은 [Clr 호스팅 환경](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)을 참조 하세요. 관리 되는 데이터베이스 개체에 대 한 자세한 내용은 [CLR&#41; 통합 &#40;공용 언어 런타임을 사용 하 여 데이터베이스 개체 작성](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)을 참조 하세요.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|로드된 어셈블리의 ID입니다. **Assembly_id** 를 사용 하 여 [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) 카탈로그 뷰에서 어셈블리에 대 한 자세한 정보를 조회할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] [Sys.debug](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) 카탈로그는 현재 데이터베이스의 어셈블리만 표시 합니다. **Sqs. dm_clr_loaded_assemblies** 뷰는 서버에 로드 된 모든 어셈블리를 표시 합니다.|  
|**appdomain_address**|**int**|어셈블리가 로드 되는 응용 프로그램 도메인 (**AppDomain**)의 주소입니다. 단일 사용자가 소유 하는 모든 어셈블리는 항상 동일한 **AppDomain**에 로드 됩니다. **Appdomain_address** 를 사용 하 여 [dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) 뷰에서 **appdomain** 에 대 한 추가 정보를 조회할 수 있습니다.|  
|**load_time**|**datetime**|어셈블리가 로드된 시간입니다. 이 어셈블리는 메모리가 부족할 때까지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로드 된 상태로 유지 되 고 **AppDomain**을 언로드합니다. **Load_time** 를 모니터링 하 여 메모리 부족 상태 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 발생 하는 빈도를 파악 하 고 **AppDomain**을 언로드할 수 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 **Dm_clr_loaded_assemblies 뷰 appdomain_address** 에는 **dm_clr_appdomains appdomain_address**와 다 대 일 관계가 있습니다. **Dm_clr_loaded_assemblies 뷰 assembly_id** 에는 **assembly_id**와 일 대 다 관계가 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로드되어 있는 현재 데이터베이스의 모든 어셈블리에 대한 세부 정보를 표시하는 방법을 보여 줍니다.  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 다음 예제에서는 지정 된 어셈블리가 로드 되는 **AppDomain** 의 세부 정보를 보는 방법을 보여 줍니다.  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>참고 항목  
 [공용 언어 런타임 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
