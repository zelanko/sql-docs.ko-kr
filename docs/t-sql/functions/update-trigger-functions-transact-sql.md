---
title: UPDATE()(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPDATE()_TSQL
- UPDATE()
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], UPDATE function
- testing column updates
- UPDATE function
- UPDATE() function
- detecting changes
- columns [SQL Server], change detection
- UPDATE statement [SQL Server], UPDATE function
- verifying column updates
- checking column updates
ms.assetid: 8e3be25b-2e3b-4d1f-a610-dcbbd8d72084
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 783eb070efcbafa2b8ec3685d66b080c420cc768
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65946786"
---
# <a name="update---trigger-functions-transact-sql"></a>UPDATE - 트리거 함수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  테이블 또는 뷰의 지정된 열에서 INSERT 또는 UPDATE를 시도했는지 여부를 나타내는 부울 값을 반환합니다. UPDATE()는 트리거가 특정 동작을 실행해야 하는지 여부를 테스트하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 또는 UPDATE 트리거 내의 어디서나 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>인수  
 *column*  
 INSERT 또는 UPDATE 동작 중 하나에 관해 테스트할 열의 이름입니다. 테이블 이름은 트리거의 ON 절에 지정되므로 열 이름 앞에 테이블 이름을 사용하지 마세요. 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 지원되는 모든 [데이터 형식](../../t-sql/data-types/data-types-transact-sql.md)을 지정할 수 있습니다. 단, 계산 열은 이 컨텍스트에서 사용할 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 UPDATE()는 INSERT 또는 UPDATE의 성공 여부와 관계없이 TRUE를 반환합니다.  
  
 둘 이상의 열에 대해 INSERT 또는 UPDATE 동작을 테스트하려면 별도의 UPDATE(*column*) 절을 지정하세요. COLUMNS_UPDATED를 사용하여 여러 열에 대한 INSERT 또는 UPDATE 동작을 테스트할 수도 있습니다. 이 경우 삽입 또는 업데이트된 열을 나타내는 비트 패턴이 반환됩니다.  
  
 열에 명시적인 값 또는 암시적인(NULL) 값이 삽입되었으므로 IF UPDATE는 INSERT 동작에 대해 TRUE 값을 반환합니다.  
  
> [!NOTE]  
>  IF UPDATE(*colum*n) 절은 IF, IF...ELSE 또는 WHILE 절과 같은 기능을 수행하며 BEGIN...END 블록을 사용할 수 있습니다. 자세한 내용은 [Control-of-Flow Language &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)을 참조하세요.  
  
 UPDATE(*column*)는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거 본문 내의 어디서나 사용할 수 있습니다.  
 
트리거가 열에 적용되면 열 값이 변경되지 않는 경우에도 `UPDATED` 값은 `true` 또는 `1`로 반환됩니다. 이는 의도적으로 설계된 것이며 트리거는 삽입/업데이트/삭제 작업이 허용되는지 여부를 결정하는 비즈니스 논리를 구현해야 합니다. 
  
## <a name="examples"></a>예  
 다음 예에서는 사용자가 `StateProvinceID` 테이블의 `PostalCode` 또는 `Address` 열을 업데이트하려고 하면 클라이언트에게 메시지를 출력하는 트리거를 만듭니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [COLUMNS_UPDATED&#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
