---
description: '&#x40;&#x40;IDENTITY (Transact-SQL)'
title: '@@IDENTITY(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d4c3f909144846292acf1247411582e7d9d638bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88365389"
---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40;IDENTITY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  마지막으로 삽입된 ID 값을 반환하는 시스템 함수입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@IDENTITY  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **numeric(38,0)**  
  
## <a name="remarks"></a>설명  
 INSERT, SELECT INTO 또는 대량 복사 문이 완료된 후 @@IDENTITY에는 문에 의해 생성된 마지막 ID 값이 들어 있습니다. 문이 ID 열이 있는 테이블에 영향을 주지 않은 경우에 @@IDENTITY은 NULL을 반환합니다. 여러 행이 삽입되어 여러 ID 값이 생성되면 @@IDENTITY은 마지막으로 생성된 ID 값을 반환합니다. 명령문이 ID 값을 생성하는 삽입 작업을 수행하는 트리거를 하나 이상 실행하는 경우 명령문 바로 다음에 @@IDENTITY를 호출하면 트리거로 생성된 마지막 ID 값이 반환됩니다. ID 열이 있는 테이블에 대한 삽입 동작 후에 트리거가 실행되었고 이 트리거가 ID 열이 없는 다른 테이블에 삽입을 수행하는 경우 @@IDENTITY은 첫 번째 삽입의 ID 값을 반환합니다. INSERT나 SELECT INTO 문 또는 대량 복사가 실패했거나 트랜잭션이 롤백된 경우 @@IDENTITY 값은 이전 설정으로 되돌아가지 않습니다.  
  
 문 및 트랜잭션이 실패해도 테이블의 현재 ID가 변경되고 ID 열 값 간에 간격이 생성될 수 있습니다. 테이블에 값을 삽입하려고 시도한 트랜잭션이 커밋되지 않아도 ID 값은 롤백되지 않습니다. 예를 들어 IGNORE_DUP_KEY 위반으로 인해 INSERT 문이 실패해도 테이블의 현재 ID 값은 계속 증가합니다.  
  
 @@IDENTITY, SCOPE_IDENTITY 및 IDENT_CURRENT는 모두 테이블의 IDENTITY 열에 삽입된 마지막 값을 반환한다는 점에서 서로 비슷한 함수입니다.  
  
 @@IDENTITY과 SCOPE_IDENTITY는 현재 세션의 테이블에서 생성된 마지막 ID 값을 반환합니다. 그러나 SCOPE_IDENTITY는 현재 범위 내에서만 값을 반환합니다. @@IDENTITY은 특정 범위로 제한되지 않습니다.  
  
 IDENT_CURRENT는 범위와 세션으로 제한되는 것이 아니라 지정된 테이블로 제한됩니다. IDENT_CURRENT는 모든 세션과 범위에 있는 특정 테이블에 생성된 ID 값을 반환합니다. 자세한 내용은 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)을 참조하세요.  
  
 @@IDENTITY 함수의 범위는 이 함수를 실행 중인 로컬 서버의 현재 세션입니다. 이 함수는 원격 서버 또는 연결된 서버에 적용할 수 없습니다. 다른 서버의 ID 값을 가져오려면 해당 원격 서버 또는 연결된 서버에서 저장 프로시저를 실행하고 이 저장 프로시저(원격 서버 또는 연결된 서버의 컨텍스트에서 실행 중)에서 ID 값을 수집하여 로컬 서버의 호출 연결에 반환하도록 합니다.  
  
 @@IDENTITY 값은 복제 트리거 및 저장 프로시저 내에서 사용되므로 복제로 인한 영향을 받을 수 있습니다. 열이 복제 아티클의 일부인 경우 @@IDENTITY은 사용자가 만든 가장 최근 ID를 정확하게 표시하지 않습니다. @@IDENTITY 대신 SCOPE_IDENTITY() 함수 구문을 사용할 수 있습니다. 자세한 내용은 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)를 참조하세요.  
  
> [!NOTE]  
>  복제에 사용되는 중첩 트리거 범위 내의 ID가 아니라 해당 사용자 명령문의 범위 내에서 사용되는 최신 ID를 반환할 `SCOPE_IDENTITY()` 함수를 사용하도록 호출하는 저장 프로시저 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 다시 작성해야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 ID 열(`LocationID`)이 있는 테이블에 행을 삽입하고 `@@IDENTITY`를 사용하여 새 행에 사용된 ID 값을 표시합니다.  
  
```  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT&#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
