---
title: Update () (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE()_TSQL
- UPDATE()
dev_langs: TSQL
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
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6d5b93a4f98e382ccb6504e1d20d6e974a031f86
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="update---trigger-functions-transact-sql"></a>업데이트-트리거 함수 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  테이블 또는 뷰의 지정된 열에서 INSERT 또는 UPDATE를 시도했는지 여부를 나타내는 부울 값을 반환합니다. UPDATE()는 트리거가 특정 동작을 실행해야 하는지 여부를 테스트하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 또는 UPDATE 트리거 내의 어디서나 사용할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>인수  
 *열*  
 INSERT 또는 UPDATE 동작 중 하나에 관해 테스트할 열의 이름입니다. 테이블 이름은 트리거의 ON 절에 지정되므로 열 이름 앞에 테이블 이름을 사용하지 마세요. 열 수 [데이터 형식](../../t-sql/data-types/data-types-transact-sql.md) 에서 지 원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 단, 계산 열은 이 컨텍스트에서 사용할 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 Boolean  
  
## <a name="remarks"></a>주의  
 UPDATE()는 INSERT 또는 UPDATE의 성공 여부와 관계없이 TRUE를 반환합니다.  
  
 둘 이상의 열에 대 한 INSERT 또는 UPDATE 동작을 테스트 하려면 별도 업데이트를 지정 합니다 (*열*) 다음에 오는 첫 번째 절. COLUMNS_UPDATED를 사용하여 여러 열에 대한 INSERT 또는 UPDATE 동작을 테스트할 수도 있습니다. 이 경우 삽입 또는 업데이트된 열을 나타내는 비트 패턴이 반환됩니다.  
  
 열에 명시적인 값 또는 암시적인(NULL) 값이 삽입되었으므로 IF UPDATE는 INSERT 동작에 대해 TRUE 값을 반환합니다.  
  
> [!NOTE]  
>  IF UPDATE (*열*n) 하는 경우 IF와 동일한 절 기능 중... 그렇지 않으면, 또는 WHILE 절 시작을 사용할 수 있습니다... 끝 블록입니다. 자세한 내용은 참조 [흐름 제어 언어 &#40; Transact SQL &#41; ](~/t-sql/language-elements/control-of-flow.md).  
  
 업데이트 (*열*)의 본문 내의 어디서 나 사용할 수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 트리거.  
  
## <a name="examples"></a>예  
 다음 예에서는 사용자가 `StateProvinceID` 테이블의 `PostalCode` 또는 `Address` 열을 업데이트하려고 하면 클라이언트에게 메시지를 출력하는 트리거를 만듭니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [COLUMNS_UPDATED &#40; Transact SQL &#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
