---
description: sp_helpindex(Transact-SQL)
title: sp_helpindex (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpindex_TSQL
- sp_helpindex
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpindex
ms.assetid: c7f73ba0-ec35-4b10-aa5f-f1487e51fbf7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a011e8f19650dad1c52b4a88e81edf28eb0bfc47
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462694"
---
# <a name="sp_helpindex-transact-sql"></a>sp_helpindex(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  테이블 또는 뷰의 인덱스에 관한 정보를 보고합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpindex [ @objname = ] 'name'  
```  
  
## <a name="arguments"></a>인수  
`[ @objname = ] 'name'` 사용자 정의 테이블 또는 뷰의 정규화 된 이름 또는 정규화 되지 않은 이름입니다. 정규화된 테이블 또는 뷰 이름이 지정된 경우에만 따옴표가 필요합니다. 데이터베이스 이름을 포함한 정규화된 이름인 경우 반드시 현재 데이터베이스의 이름을 사용해야 합니다. *name* 은 **nvarchar (776)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**index_name**|**sysname**|인덱스 이름입니다.|  
|**index_description**|**varchar (210)**|인덱스가 있는 파일 그룹을 포함하는 인덱스 설명입니다.|  
|**index_keys**|**nvarchar (2078)**|인덱스가 만들어진 테이블 또는 뷰의 열입니다.|  
  
 내림차순으로 인덱스가 만들어진 열은 이름 옆에 빼기 표시(-)를 한 상태로 결과 집합에 나열됩니다. 기본값인 오름차순으로 인덱스가 만들어진 열은 이름만 나열됩니다.  
  
## <a name="remarks"></a>설명  
 통계 업데이트의 NORECOMPUTE 옵션을 사용 하 여 인덱스를 설정 하면 해당 정보가 **index_description** 열에 포함 됩니다.  
  
 **sp_helpindex** 는 정렬 가능 인덱스 열만 노출 합니다. 따라서 XML 인덱스 또는 공간 인덱스에 대 한 정보를 노출 하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Customer` 테이블에 관한 인덱스의 유형을 보고합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpindex N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
