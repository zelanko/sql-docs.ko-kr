---
title: '@@IDENTITY (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88cdaa1362e5d60b0f880c66c7fb7038ddb9f126
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40identity-transact-sql"></a>& #x 40; & &#40;x; IDENTITY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  마지막으로 삽입된 ID 값을 반환하는 시스템 함수입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>반환 형식  
 **38, 0**  
  
## <a name="remarks"></a>주의  
 INSERT, SELECT INTO 또는 대량 복사 문이 완료 되 면 @@IDENTITY 문에 의해 생성 된 마지막 id 값을 포함 합니다. 문이 않은 영향을 주지 id 열이 있는 테이블@IDENTITY NULL을 반환 합니다. 여러 행을 삽입 한 경우 여러 id 값을 생성@IDENTITY 생성 된 마지막 id 값을 반환 합니다. 문이 id 값을 생성 하는 삽입을 수행 하는 트리거를 하나 이상 발생 하는 경우 호출@IDENTITY 하면 트리거로 생성 된 마지막 id 값 반환 후에 즉시 합니다. Id 열이 있는 테이블에 대 한 삽입 작업 후에 트리거가 발생 하 고 트리거 @ id 열이 없는 다른 테이블에 삽입 하는 경우@IDENTITY 첫 번째 삽입의 id 값을 반환 합니다. @@IDENTITY 값 트랜잭션이 롤백되는 경우 또는 INSERT 나 SELECT INTO 문 또는 대량 복사에 실패 하면 이전 설정으로 되돌아가지 않습니다.  
  
 문 및 트랜잭션이 실패해도 테이블의 현재 ID가 변경되고 ID 열 값 간에 간격이 생성될 수 있습니다. 테이블에 값을 삽입하려고 시도한 트랜잭션이 커밋되지 않아도 ID 값은 롤백되지 않습니다. 예를 들어 IGNORE_DUP_KEY 위반으로 인해 INSERT 문이 실패해도 테이블의 현재 ID 값은 계속 증가합니다.  
  
 @@IDENTITY, SCOPE_IDENTITY 및 IDENT_CURRENT는 비슷한 함수 모두 테이블의 ID 열에 삽입 된 마지막 값을 반환 합니다.  
  
 @@IDENTITY SCOPE_IDENTITY는 현재 세션의 모든 테이블에서 생성 된 마지막 id 값을 반환 하 고 있습니다. SCOPE_IDENTITY는 현재 범위 내 에서만 값을 반환 하는 반면 @@IDENTITY 특정 범위로 제한 되지 않습니다.  
  
 IDENT_CURRENT는 범위와 세션으로 제한되는 것이 아니라 지정된 테이블로 제한됩니다. IDENT_CURRENT는 모든 세션과 범위에 있는 특정 테이블에 생성된 ID 값을 반환합니다. 자세한 내용은 참조 [IDENT_CURRENT &#40; Transact SQL &#41; ](../../t-sql/functions/ident-current-transact-sql.md).  
  
 범위는 @@IDENTITY 함수 실행은 로컬 서버에서 현재 세션입니다. 이 함수는 원격 서버 또는 연결된 서버에 적용할 수 없습니다. 다른 서버의 ID 값을 가져오려면 해당 원격 서버 또는 연결된 서버에서 저장 프로시저를 실행하고 이 저장 프로시저(원격 서버 또는 연결된 서버의 컨텍스트에서 실행 중)에서 ID 값을 수집하여 로컬 서버의 호출 연결에 반환하도록 합니다.  
  
 복제에 영향을 줄 수는 @@IDENTITY 값을 복제 트리거 및 저장된 프로시저 내에서 사용 되기 때문입니다. @@IDENTITY 열이 복제 아티클의 일부인 경우 사용자가 만든 가장 최근 id 정확 하 게 표시 하지 않습니다. @ 대신 scope_identity () 함수 구문을 사용할 수 있습니다@IDENTITY합니다. 자세한 내용은 참조 [SCOPE_IDENTITY &#40; Transact SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  호출 하는 저장 프로시저 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용 하도록 문을 다시 작성 해야는 `SCOPE_IDENTITY()` 해당 사용자 문의 범위 내에서 사용 되는 최신 id 및에서 사용 되는 중첩된 트리거 범위 내에서 id가 아닌 반환 하는 함수를 복제 합니다.  
  
## <a name="examples"></a>예  
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
  
## <a name="see-also"></a>관련 항목:  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT&#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40; Transact SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

