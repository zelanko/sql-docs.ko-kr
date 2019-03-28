---
title: sp_helpfile (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpfile
- sp_helpfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpfile
ms.assetid: 1546e0ae-5a99-4e01-9eb9-d147fa65884c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6447f9a8a8504539400154c29c34d7340fcdb2d8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536305"
---
# <a name="sphelpfile-transact-sql"></a>sp_helpfile(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스와 연결된 파일의 물리적 이름 및 특성을 반환합니다. 서버에 첨부하거나 서버에서 분리할 파일의 이름을 결정하는 데 이 저장 프로시저를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @filename = ] 'name'` 현재 데이터베이스에 있는 파일의 논리적 이름이입니다. *이름* 됩니다 **sysname**, 기본값은 NULL입니다. 하는 경우 *이름을* 은 지정 하지 않으면 현재 데이터베이스의 모든 파일의 특성이 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|논리적 파일 이름입니다.|  
|**fileid**|**smallint**|파일의 숫자 식별자입니다. 경우에 반환 되지 않습니다 *이름을* 된*합니다.*|  
|**filename**|**nchar(260)**|물리적 파일 이름입니다.|  
|**filegroup**|**sysname**|파일이 속한 파일 그룹입니다.<br /><br /> NULL = 파일이 로그 파일입니다. 파일 그룹에 속하지 않습니다.|  
|**size**|**nvarchar(15)**|파일 크기(KB)입니다.|  
|**maxsize**|**nvarchar(15)**|파일이 증가할 수 있는 최대 크기입니다. 이 필드 값이 UNLIMITED이면 디스크가 꽉 찰 때까지 파일이 증가할 수 있음을 의미합니다.|  
|**growth**|**nvarchar(15)**|파일의 증가분입니다. 공간이 새로 필요할 때마다 파일에 추가되는 공간의 양을 나타냅니다.<br /><br /> 0 = 파일은 고정 크기를 가지며 증가하지 않습니다.|  
|**usage**|**varchar(9)**|데이터 파일에 대 한 값이 **'데이터만'** 하 고 값은 로그 파일에 대 한 **'로그'** 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]에 있는 파일에 대한 정보를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_helpfile;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_helpfilegroup&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
