---
title: sys.dm_clr_loaded_assemblies (TRANSACT-SQL) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138663"
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버 주소 공간으로 로드되는 각각의 관리되는 사용자 어셈블리에 대해 행을 반환합니다. 이 뷰를 이해 하 고 CLR 통합 문제 해결 관리 되는 실행 되 고 있는 데이터베이스 개체 사용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 어셈블리는 관리되는 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 정의 및 배포하는 데 사용되는 관리 코드 DLL 파일입니다. 사용자가 이러한 관리되는 데이터베이스 개체 중 하나를 실행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 CLR은 관리되는 데이터베이스 개체가 정의되는 어셈블리 및 해당 참조를 로드합니다. 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드된 상태로 유지되어 성능을 향상시키므로 어셈블리에 포함된 관리되는 데이터베이스 개체가 어셈블리를 다시 로드하지 않고 나중에 호출될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 메모리가 부족해질 때까지 어셈블리가 언로드되지 않습니다. 참조 어셈블리 및 CLR 통합에 대 한 자세한 내용은 [CLR 호스팅 환경](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)합니다. 관리 되는 데이터베이스 개체에 대 한 자세한 내용은 참조 하세요. [공용 언어 런타임을 사용 하 여 데이터베이스 개체 작성 &#40;CLR&#41; 통합](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)합니다.  

  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|로드된 어셈블리의 ID입니다. 합니다 **assembly_id** 에서 어셈블리에 대 한 자세한 정보를 조회할 수는 [sys.assemblies &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) 카탈로그 뷰. 유의 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) 카탈로그는 현재 데이터베이스에서 어셈블리를 보여 줍니다. 합니다 **sqs.dm_clr_loaded_assemblies** 보기 서버에 로드 된 모든 어셈블리를 표시 합니다.|  
|**appdomain_address**|**int**|응용 프로그램 도메인의 주소 (**AppDomain**)에서 어셈블리를 로드 합니다. 단일 사용자가 소유한 모든 어셈블리는 항상 동일한 로드 **AppDomain**합니다. **appdomain_address** 에 대 한 자세한 정보를 조회에 사용할 수는 **AppDomain** 에 [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) 보기.|  
|**load_time**|**datetime**|어셈블리가 로드된 시간입니다. 어셈블리 로드 될 때까지 상태로 유지 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리가 부족 하 고 언로드합니다 합니다 **AppDomain**합니다. 모니터링할 수 있습니다 **load_time** 빈도 이해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리가 부족 하 고 언로드합니다 합니다 **AppDomain**합니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="remarks"></a>설명  
 합니다 **dm_clr_loaded_assemblies.appdomain_address** 보기와 다 대 일 관계가 **dm_clr_appdomains.appdomain_address**합니다. 합니다 **dm_clr_loaded_assemblies.assembly_id** 보기에 일 대 다 관계를 갖고 **sys.assemblies.assembly_id**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로드되어 있는 현재 데이터베이스의 모든 어셈블리에 대한 세부 정보를 표시하는 방법을 보여 줍니다.  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 다음 예제에서는의 세부 정보를 보는 방법 합니다 **AppDomain** 에서 지정 된 어셈블리를 로드 합니다.  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>관련 항목  
 [공용 언어 런타임 관련 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
