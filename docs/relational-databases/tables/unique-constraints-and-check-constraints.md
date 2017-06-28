---
title: "UNIQUE 제약 조건 및 CHECK 제약 조건 | Microsoft 문서"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b5596207dc1188bd9830c0993402194954737c6a
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="unique-constraints-and-check-constraints"></a>UNIQUE 제약 조건 및 CHECK 제약 조건
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에서 데이터 무결성을 강제 적용하는 데 사용할 수 있는 두 가지 유형의 제약 조건으로 UNIQUE 제약 조건과 CHECK 제약 조건이 있습니다. 이들 키는 중요한 데이터베이스 개체입니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [UNIQUE 제약 조건](#Unique)  
  
 [CHECK 제약 조건](#Check)  
  
 [관련 태스크](#Tasks)  
  
##  <a name="Unique"></a> UNIQUE 제약 조건  
 제약 조건은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서 사용자에게 적용하는 규칙입니다. 예를 들어 UNIQUE 제약 조건을 사용하면 기본 키에 참여하고 있지 않은 특정 열에 중복 값이 입력되지 않도록 할 수 있습니다. UNIQUE 제약 조건과 PRIMARY KEY 제약 조건이 모두 고유성을 강제 적용하지만 기본 키가 아닌 열 또는 열 조합에 대해 고유성을 강제 적용하려면 PRIMARY KEY 제약 조건 대신 UNIQUE 제약 조건을 사용하세요.  
  
 PRIMARY KEY 제약 조건과 달리 UNIQUE 제약 조건에서는 NULL 값이 허용됩니다. 단 UNIQUE 제약 조건에서 사용되는 다른 값과 마찬가지로 Null 값도 열당 하나만 허용됩니다. UNIQUE 제약 조건은 FOREIGN KEY 제약 조건에서 참조할 수 있습니다.  
  
 테이블의 기존 열에 UNIQUE 제약 조건이 추가되면 기본적으로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 열의 기존 데이터를 검사하여 모든 값이 고유한지 확인합니다. 중복된 값이 있는 열에 UNIQUE 제약 조건을 추가하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 오류를 반환하고 제약 조건이 추가되지 않습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 자동으로 UNIQUE 인덱스를 만들어 UNIQUE 제약 조건의 고유성 요구 사항을 적용합니다. 따라서 중복 행을 삽입하려고 하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 UNIQUE 제약 조건을 위반하여 테이블에 행을 추가할 수 없다는 오류 메시지가 반환됩니다. 클러스터형 인덱스가 명시적으로 지정되지 않는 한 고유한 비클러스터형 인덱스가 기본적으로 생성되어 UNIQUE 제약 조건을 적용합니다.  
  
##  <a name="Check"></a> CHECK 제약 조건  
 CHECK 제약 조건은 하나 이상의 열에서 허용되는 값을 제한하여 도메인 무결성을 강제 적용합니다. 논리 연산자에 따라 TRUE 또는 FALSE를 반환하는 논리(부울) 식을 사용하여 CHECK 제약 조건을 만들 수 있습니다. 예를 들어 15,000달러부터 100,000달러까지의 데이터만 허용하는 CHECK 제약 조건을 만들어 **salary** 열의 값 범위를 제한할 수 있습니다. 이렇게 하면 정상 월급 범위를 벗어나는 월급은 입력되지 않습니다. 논리 식은 다음과 같습니다. `salary >= 15000 AND salary <= 100000`  
  
 열 하나에 여러 개의 CHECK 제약 조건을 적용할 수 있습니다. 테이블 수준에서 CHECK 제약 조건을 만들어 여러 열에 적용할 수도 있습니다. 예를 들어 여러 열에 대한 CHECK 제약 조건을 사용하여 **country_region** 열 값이 **USA** 인 모든 행이 **state** 열에서 두 문자의 값을 갖도록 할 수 있습니다. 이렇게 한 위치에서 여러 조건을 검사할 수 있습니다.  
  
 CHECK 제약 조건은 열에 있는 값을 다룬다는 점에서는 FOREIGN KEY 제약 조건과 비슷합니다. 어떤 값이 유효한지 결정하는 방법은 서로 다릅니다. FOREIGN KEY 제약 조건은 다른 테이블로부터 유효한 값을 가져오는 반면 CHECK 제약 조건은 논리 식으로부터 유효한 값을 결정합니다.  
  
> [!CAUTION]  
>  제약 조건에 암시적 또는 명시적 데이터 형식 변환이 포함된 경우 특정 작업이 실패할 수 있습니다. 예를 들어 파티션 전환의 원본인 테이블에 정의된 이러한 제약 조건으로 인해 ALTER TABLE...SWITCH 작업이 실패할 수 있습니다. 제약 조건 정의에서 데이터 형식을 변환하지 마세요.  
  
### <a name="limitations-of-check-constraints"></a>CHECK 제약 조건의 제한 사항  
 CHECK 제약 조건은 FALSE로 평가되는 값을 거부합니다. Null 값은 UNKNOWN으로 평가되므로 식에 Null 값이 있으면 제약 조건이 무시됩니다. 예를 들어 **MyColumn=10** 과 같이 **MyColumn** 에 값 10만 포함할 수 있도록 **int** 열**MyColumn**에 대한 제약 조건을 지정한다고 가정합니다. **MyColumn**에 NULL 값을 삽입할 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 NULL을 삽입하고 오류를 반환하지 않습니다.  
  
 CHECK 제약 조건은 확인 중인 조건이 테이블의 모든 행에 대해 FALSE가 아니면 TRUE를 반환합니다. CHECK 제약 조건은 행 수준에서 작동합니다. 방금 만든 테이블에 행이 없어도 이 테이블의 CHECK 제약 조건은 유효한 것으로 간주됩니다. 다음 예와 같이 이러한 상황은 예기치 않은 결과를 생성할 수 있습니다.  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 추가 중인 `CHECK` 제약 조건은 `CheckTbl`테이블에 행이 적어도 하나 이상 있어야 함을 지정합니다. 그러나 이 제약 조건이 적용되는 테이블에 행이 없기 때문에 ALTER TABLE 문이 성공합니다.  
  
 DELETE 문을 실행하는 동안에는 CHECK 제약 조건이 확인되지 않습니다. 따라서 특정 유형의 CHECK 제약 조건이 있는 테이블에 대해 DELETE 문을 실행하면 예기치 않은 결과가 생성될 수 있습니다. 예를 들어 `CheckTbl`테이블에서 다음 문을 실행하는 경우를 살펴봅니다.  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 `DELETE` 제약 조건에서 `CHECK` 테이블에 행이 적어도 `CheckTbl` 개 이상 있어야 한다고 지정해도 `1` 문이 성공합니다.  
  
##  <a name="Tasks"></a> 관련 태스크  
  
> [!NOTE]  
>  테이블이 복제용으로 게시된 경우 Transact-SQL 문 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) 또는 SMO(SQL Server 관리 개체)를 사용하여 스키마를 변경해야 합니다. 테이블 디자이너 또는 데이터베이스 다이어그램 디자이너를 사용하여 스키마를 변경하면 테이블 삭제 및 재생성이 시도됩니다. 게시된 개체를 삭제할 수 없으므로 스키마가 변경되지 않습니다.  
  
|태스크|항목|  
|----------|-----------|  
|UNIQUE 제약 조건을 만드는 방법에 대해 설명합니다.|[UNIQUE 제약 조건 만들기](../../relational-databases/tables/create-unique-constraints.md)|  
|UNIQUE 제약 조건을 수정하는 방법에 대해 설명합니다.|[UNIQUE 제약 조건 수정](../../relational-databases/tables/modify-unique-constraints.md)|  
|UNIQUE 제약 조건을 삭제하는 방법에 대해 설명합니다.|[UNIQUE 제약 조건 삭제](../../relational-databases/tables/delete-unique-constraints.md)|  
|복제 에이전트가 테이블에 데이터를 삽입 또는 업데이트하는 경우 CHECK 제약 조건을 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[복제할 때 CHECK 제약 조건 해제](../../relational-databases/tables/disable-check-constraints-for-replication.md)|  
|테이블에서 데이터를 추가, 업데이트 또는 삭제할 때 CHECK 제약 조건을 사용하지 않도록 설정하는 방법에 대해 설명합니다.|[INSERT 및 UPDATE 문에서 CHECK 제약 조건 해제](../../relational-databases/tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|제약 조건 식 또는 특정 조건에 따라 제약 조건을 사용하거나 사용할 수 없게 하는 옵션을 변경하는 방법에 대해 설명합니다.|[CHECK 제약 조건 수정](../../relational-databases/tables/modify-check-constraints.md)|  
|CHECK 제약 조건을 삭제하는 방법에 대해 설명합니다.|[CHECK 제약 조건 삭제](../../relational-databases/tables/delete-check-constraints.md)|  
|CHECK 제약 조건의 속성을 보는 방법에 대해 설명합니다.|[UNIQUE 제약 조건 및 CHECK 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md)|  
  
  

