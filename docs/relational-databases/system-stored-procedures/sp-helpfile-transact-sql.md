---
title: sp_helpfile (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 812be95c9584e75d8452c946d1935625468a79a1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828338"
---
# <a name="sp_helpfile-transact-sql"></a>sp_helpfile(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스와 연결된 파일의 물리적 이름 및 특성을 반환합니다. 서버에 첨부하거나 서버에서 분리할 파일의 이름을 결정하는 데 이 저장 프로시저를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpfile [ [ @filename= ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @filename = ] 'name'`현재 데이터베이스에 있는 모든 파일의 논리적 이름입니다. *name* 은 **sysname**이며 기본값은 NULL입니다. *Name* 을 지정 하지 않으면 현재 데이터베이스에 있는 모든 파일의 특성이 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|논리적 파일 이름입니다.|  
|**fileid**|**smallint**|파일의 숫자 식별자입니다. *Name* 이 지정 된 경우이 반환 되지 않습니다 *.*|  
|**이름도**|**nchar (260)**|물리적 파일 이름입니다.|  
|**그룹별로**|**sysname**|파일이 속한 파일 그룹입니다.<br /><br /> NULL = 파일이 로그 파일입니다. 파일 그룹에 속하지 않습니다.|  
|**size**|**nvarchar (15)**|파일 크기(KB)입니다.|  
|**크기**|**nvarchar (15)**|파일이 증가할 수 있는 최대 크기입니다. 이 필드 값이 UNLIMITED이면 디스크가 꽉 찰 때까지 파일이 증가할 수 있음을 의미합니다.|  
|**growth**|**nvarchar (15)**|파일의 증가분입니다. 공간이 새로 필요할 때마다 파일에 추가되는 공간의 양을 나타냅니다.<br /><br /> 0 = 파일은 고정 크기를 가지며 증가하지 않습니다.|  
|**보려면**|**varchar (9)**|데이터 파일의 경우 값은 **' 데이터 전용 '** 이 고, 로그 파일의 경우 값은 **' 로그 전용 '** 입니다.|  
  
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
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_helpfilegroup &#40;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [database_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [master_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [sys. 파일 그룹 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
