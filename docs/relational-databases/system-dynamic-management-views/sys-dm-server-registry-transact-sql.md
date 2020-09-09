---
description: sys.dm_server_registry(Transact-SQL)
title: sys. dm_server_registry (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 48fc4cbb0967e757308d876a68d3580bcf72c4c6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89530645"
---
# <a name="sysdm_server_registry-transact-sql"></a>sys.dm_server_registry(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 인스턴스에 대한 Windows 레지스트리에 저장된 구성 및 설치 정보를 반환합니다. 각 레지스트리 키에 대해 행을 하나씩 반환합니다. 이 동적 관리 뷰를 사용하면 호스트 컴퓨터에서 사용 가능한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 네트워크 구성 값 같은 정보를 반환할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|registry_key|**nvarchar(256)**|레지스트리 키 이름입니다. Null을 허용합니다.|  
|value_name|**nvarchar(256)**|키 값 이름이며 레지스트리 편집기의 **이름** 열에 표시 되는 항목입니다. Null을 허용합니다.|  
|value_data|**sql_variant**|키 데이터의 값이며 지정 된 항목에 대 한 레지스트리 편집기의 **데이터** 열에 표시 되는 값입니다. Null을 허용합니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-display-the-sql-server-services"></a>A. SQL Server 서비스 표시  
 다음 예에서는 SQL Server의 현재 인스턴스에 대한 SQL Server 및 SQL Server 에이전트 서비스의 레지스트리 키 값을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%ControlSet%';  
```  
  
### <a name="b-display-the-sql-server-agent-registry-key-values"></a>B. SQL Server 에이전트 레지스트리 키 값 표시  
 다음 예에서는 SQL Server의 현재 인스턴스에 대한 SQL Server 에이전트 레지스트리 키 값을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SQLAgent%';  
```  
  
### <a name="c-display-the-current-version-of-the-instance-of-sql-server"></a>C. SQL Server 인스턴스의 현재 버전 표시  
 다음 예에서는 SQL Server의 현재 인스턴스 버전을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE value_name = N'CurrentVersion';  
```  
  
### <a name="d-display-the-parameters-passed-to-the-instance-of-sql-server-during-startup"></a>D. 시작 시 SQL Server 인스턴스에 전달되는 매개 변수 표시  
 다음 예에서는 시작 시 SQL Server 인스턴스에 전달되는 매개 변수를 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%Parameters';  
```  
  
### <a name="e-return-network-configuration-information-for-the-instance-of-sql-server"></a>E. SQL Server 인스턴스의 네트워크 구성 정보 반환  
 다음 예에서는 SQL Server의 현재 인스턴스에 대한 네트워크 구성 값을 반환합니다.  
  
```  
SELECT registry_key, value_name, value_data  
FROM sys.dm_server_registry  
WHERE registry_key LIKE N'%SuperSocketNetLib%';  
```  
  
## <a name="see-also"></a>참고 항목  
 [dm_server_services &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md)  
  
  
