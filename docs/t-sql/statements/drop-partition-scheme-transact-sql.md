---
title: DROP PARTITION SCHEME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP PARTITION SCHEME
- DROP_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP PARTITION SCHEME statement
- deleting partition schemes
- dropping partition schemes
- removing partition schemes
- partition schemes [SQL Server], removing
ms.assetid: 6efbc87c-1c92-4e43-96a7-e0f30f1db185
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5443e982d82374cc5ba7848a3792c4162397f26e
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81635297"
---
# <a name="drop-partition-scheme-transact-sql"></a>DROP PARTITION SCHEME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 파티션 구성표를 제거합니다. [CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)을 사용하여 파티션 스키마를 만들고 [ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)을 사용하여 파티션 스키마를 수정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DROP PARTITION SCHEME partition_scheme_name [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *partition_scheme_name*  
 삭제할 파티션 스키마의 이름입니다.  
  
## <a name="remarks"></a>설명  
 현재 파티션 스키마를 사용하는 테이블이나 인덱스가 없는 경우에만 파티션 스키마를 삭제할 수 있습니다. 파티션 스키마를 사용하는 테이블이나 인덱스가 있는 경우 DROP PARTITION SCHEME에서 오류를 반환합니다. DROP PARTITION SCHEME이 파일 그룹 자체를 제거하는 것은 아닙니다.  
  
## <a name="permissions"></a>사용 권한  
 DROP PARTITION SCHEME을 실행하는 데 다음 권한을 사용할 수 있습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 구성표가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 구성표가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에서 `myRangePS1` 파티션 스키마를 삭제하는 방법을 보여 줍니다.  
  
```  
DROP PARTITION SCHEME myRangePS1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [sys.partition_schemes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
