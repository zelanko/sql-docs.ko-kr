---
title: sys.dm_server_registry (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_server_registry_TSQL
- sys.dm_server_registry
- dm_server_registry
- sys.dm_server_registry_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_registry dynamic management view
ms.assetid: 9b3e0c74-2e99-4996-a383-104d51831e97
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e5864e303413b8dfe8027746f92726c5add5a4d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmserverregistry-transact-sql"></a>sys.dm_server_registry(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 대한 Windows 레지스트리에 저장된 구성 및 설치 정보를 반환합니다. 각 레지스트리 키에 대해 행을 하나씩 반환합니다. 이 동적 관리 뷰를 사용하면 호스트 컴퓨터에서 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 네트워크 구성 값 같은 정보를 반환할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|레지스트리 키 이름입니다. Null을 허용합니다.|  
|value_name|**nvarchar(256)**|키 값 이름이며 이것은에 표시 된 항목의 **이름** 레지스트리 편집기의 열입니다. Null을 허용합니다.|  
|value_data|**sql_variant**|키 데이터의 값이며 에 표시 된 값이 고 **데이터** 지정된 된 항목에 대 한 레지스트리 편집기의 열입니다. Null을 허용합니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-display-the-sql-server-services"></a>1. SQL Server 서비스 표시  
 다음 예에서는 SQL Server의 현재 인스턴스에 대한 SQL Server 및 SQL Server 에이전트 서비스의 레지스트리 키 값을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%ControlSet%';  
```  
  
### <a name="b-display-the-sql-server-agent-registry-key-values"></a>2. SQL Server 에이전트 레지스트리 키 값 표시  
 다음 예에서는 SQL Server의 현재 인스턴스에 대한 SQL Server 에이전트 레지스트리 키 값을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SQLAgent%';  
```  
  
### <a name="c-display-the-current-version-of-the-instance-of-sql-server"></a>3. SQL Server 인스턴스의 현재 버전 표시  
 다음 예에서는 SQL Server의 현재 인스턴스 버전을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key = N'CurrentVersion';  
```  
  
### <a name="d-display-the-parameters-passed-to-the-instance-of-sql-server-during-startup"></a>4. 시작 시 SQL Server 인스턴스에 전달되는 매개 변수 표시  
 다음 예에서는 시작 시 SQL Server 인스턴스에 전달되는 매개 변수를 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%Parameters';  
```  
  
### <a name="e-return-network-configuration-information-for-the-instance-of-sql-server"></a>5. SQL Server 인스턴스의 네트워크 구성 정보 반환  
 다음 예에서는 SQL Server의 현재 인스턴스에 대한 네트워크 구성 값을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SuperSocketNetLib%';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_server_services &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  
