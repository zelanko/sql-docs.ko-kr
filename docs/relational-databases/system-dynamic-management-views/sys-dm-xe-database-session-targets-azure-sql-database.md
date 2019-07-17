---
title: sys.dm_xe_database_session_targets (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
author: MightyPen
ms.author: genemi
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 60d26d76f4d158799fe52e28be9927744ca98745
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090424"
---
# <a name="sysdmxedatabasesessiontargets-azure-sql-database"></a>sys.dm_xe_database_session_targets(Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  세션 대상에 대한 정보를 반환합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 및 향후 버전입니다.|  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|이벤트 세션의 메모리 주소입니다. Sys.dm_xe_database_sessions.address 사용 하 여 다 대 일 관계가 있습니다. Null을 허용하지 않습니다.|  
|target_name|**nvarchar(60)**|세션 내에 있는 대상의 이름입니다. Null을 허용하지 않습니다.|  
|target_package_guid|**uniqueidentifier**|대상이 포함된 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|execution_count|**bigint**|세션에 대해 대상이 실행된 횟수입니다. Null을 허용하지 않습니다.|  
|execution_duration_ms|**bigint**|대상이 실행된 총 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|target_data|**nvarchar(max)**|이벤트 집계 정보와 같이 대상에서 유지 관리하는 데이터입니다. Null을 허용합니다.|  
  
## <a name="permissions"></a>사용 권한  
 VIEW DATABASE STATE 권한이 필요합니다.  
  
### <a name="relationship-cardinalities"></a>관계 카디널리티  
  
|보낸 사람|수행할 작업|관계|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_targets.event_session_address|sys.dm_xe_database_sessions.address|다 대 일|  
  
  
