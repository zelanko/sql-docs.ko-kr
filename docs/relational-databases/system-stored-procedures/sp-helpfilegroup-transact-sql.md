---
description: sp_helpfilegroup(Transact-SQL)
title: sp_helpfilegroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfilegroup_TSQL
- sp_helpfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfilegroup
ms.assetid: 619716b5-95dc-4538-82ae-4b90b9da8ebc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 253118a01b4044d752c16e570e16b1f46f21ede2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549623"
---
# <a name="sp_helpfilegroup-transact-sql"></a>sp_helpfilegroup(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스와 연관된 파일 그룹의 이름과 특성을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpfilegroup [ [ @filegroupname = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @filegroupname = ] 'name'` 현재 데이터베이스에 있는 모든 파일 그룹의 논리적 이름입니다. *name* 은 **sysname**이며 기본값은 NULL입니다. *Name* 을 지정 하지 않으면 현재 데이터베이스의 모든 파일 그룹이 나열 되며 결과 집합 섹션에 표시 된 첫 번째 결과 집합만 표시 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**groupname**|**sysname**|파일 그룹의 이름입니다.|  
|**groupid**|**smallint**|파일 그룹의 숫자 ID입니다.|  
|**filecount**|**int**|파일 그룹의 파일 수입니다.|  
  
 *Name* 을 지정 하면 파일 그룹의 각 파일에 대해 한 개의 행이 반환 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**file_in_group**|**sysname**|파일 그룹에 있는 파일의 논리적 이름입니다.|  
|**fileid**|**smallint**|파일의 숫자 ID입니다.|  
|**filename**|**nchar (260)**|디렉터리 경로를 포함한 파일의 물리적 이름입니다.|  
|**size**|**nvarchar (15)**|파일 크기(KB)입니다.|  
|**크기**|**nvarchar (15)**|파일의 최대 크기입니다.<br /><br /> 파일이 증가할 수 있는 최대 크기입니다. 이 필드 값이 UNLIMITED이면 디스크가 꽉 찰 때까지 파일이 증가할 수 있음을 의미합니다.|  
|**성장은**|**nvarchar (15)**|파일의 증가분입니다. 공간이 새로 필요할 때마다 파일에 추가되는 공간의 양을 나타냅니다.<br /><br /> 0 = 파일은 고정 크기를 가지며 증가하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-all-filegroups-in-a-database"></a>A. 데이터베이스에 있는 모든 파일 그룹 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에 있는 파일 그룹에 대한 정보를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup;  
GO  
```  
  
### <a name="b-returning-all-files-in-a-filegroup"></a>B. 파일 그룹에 있는 모든 파일 반환  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스의 `PRIMARY` 파일 그룹에 있는 모든 파일에 대한 정보를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfilegroup 'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_helpfile &#40;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [master_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
