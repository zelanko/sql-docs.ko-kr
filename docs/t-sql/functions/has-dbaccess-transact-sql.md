---
description: HAS_DBACCESS(Transact-SQL)
title: HAS_DBACCESS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HAS_DBACCESS_TSQL
- HAS_DBACCESS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- permissions [SQL Server], user access status
- HAS_DBACCESS
- checking permission status
- verifying permission status
- users [SQL Server], access rights status
- testing permissions
- status information [SQL Server], user access
ms.assetid: 99b43a72-0722-4a7b-a493-bdee1c74c7b9
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2ba9047673e7f43202ec74f577e039d3b769abe
ms.sourcegitcommit: 76d31f456982dabb226239b424eaa7139d8cc6c1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90570624"
---
# <a name="has_dbaccess-transact-sql"></a>HAS_DBACCESS(Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  지정된 데이터베이스를 사용자가 액세스할 수 있는지에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
HAS_DBACCESS ( 'database_name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 '*database_name*'  
 사용자가 액세스 정보를 얻으려고 하는 데이터베이스의 이름입니다. *database_name*은 **sysname**입니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>설명  
 HAS_DBACCESS는 사용자가 데이터베이스에 액세스할 수 있으면 1을 반환하고 사용자가 데이터베이스에 액세스할 수 없으면 0을 반환하며 데이터베이스 이름이 잘못되었으면 NULL을 반환합니다.  
  
 HAS_DBACCESS는 데이터베이스가 오프라인 또는 주의 대상이면 0을 반환합니다.  
  
 HAS_DBACCESS는 데이터베이스가 단일 사용자 모드에 있고 다른 사용자가 데이터베이스를 사용 중이면 0을 반환합니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 사용자가 `AdventureWorks2012` 데이터베이스에 액세스할 수 있는지 테스트하는 방법을 보여 줍니다.  
  
```sql  
SELECT HAS_DBACCESS('AdventureWorks2012');  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 현재 사용자가 `AdventureWorksPDW2012` 데이터베이스에 액세스할 수 있는지 테스트하는 방법을 보여 줍니다.  
  
```sql  
SELECT HAS_DBACCESS('AdventureWorksPDW2012');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [IS_MEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)  
  
  

