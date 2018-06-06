---
title: 사용자 정의 함수 | Microsoft 문서
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: udf
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-udf
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cc7cf4ed368b63c7b070873dda3d23fcce909f35
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34709001"
---
# <a name="user-defined-functions"></a>사용자 정의 함수
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  프로그래밍 언어의 함수처럼 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 정의 함수는 매개 변수를 받아들이고 복잡한 계산과 같은 동작을 수행하며 해당 작업의 결과를 값으로 반환합니다. 반환 값은 단일 스칼라 값이나 결과 집합일 수 있습니다.  
   
##  <a name="Benefits"></a> 사용자 정의 함수  
사용하는 이유 
  
-   모듈식 프로그래밍을 허용합니다.  
  
     함수를 한 번 만들어 데이터베이스에 저장한 후에는 프로그램에서 여러 번 호출할 수 있습니다. 사용자 정의 함수는 프로그램 원본 코드에 관계없이 수정할 수 있습니다.  
  
-   작업을 더 빨리 실행할 수 있습니다.  
  
     저장 프로시저와 마찬가지로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수는 계획을 캐시하고 반복 실행에 다시 사용함으로써 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드의 컴파일 비용을 줄입니다. 즉, 사용자 정의 함수를 매번 다시 구문 분석하고 최적화할 필요가 없기 때문에 더 빨리 실행할 수 있습니다.  
  
     CLR 함수는 계산 태스크, 문자열 조작 및 비즈니스 논리 면에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수보다 더 뛰어난 성공을 제공합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수는 데이터를 많이 액세스하는 논리에 더 적합합니다.  
  
-   네트워크 트래픽을 줄일 수 있습니다.  
  
     단일 스칼라 식으로 표현할 수 없는 일부 복잡한 제약 조건을 기반으로 데이터를 필터링하는 작업을 함수로 표현할 수 있습니다. 그런 다음 WHERE 절에서 이 함수를 호출하여 클라이언트에 전송되는 행 수를 줄일 수 있습니다.  
  
> [!NOTE]
> 쿼리에 포함된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 사용자 정의 함수는 단일 스레드(직렬 실행 계획)에서만 실행할 수 있습니다.  
  
##  <a name="FunctionTypes"></a> 함수 유형  
**스칼라 함수**  
 사용자 정의 스칼라 함수는 RETURNS 절에 정의된 유형의 단일 데이터 값을 반환합니다. 인라인 스칼라 함수에는 함수 본문이 없으며 스칼라 값이 단일 문의 결과입니다. 다중 문 스칼라 함수의 함수 본문은 BEGIN...END 블록으로 정의되며 여기에는 단일 값을 반환하는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 포함됩니다. 반환 유형은 **text**, **ntext**, **image**, **cursor**및 **timestamp**를 제외한 모든 데이터 형식일 수 있습니다. 
 **[예](https://msdn.microsoft.com/library/bb386973(v=vs.110).aspx)**
  
**테이블 반환 함수**  
 사용자 정의 테이블 값 함수는 **table** 데이터 형식을 반환합니다. 인라인 테이블 반환 함수에는 함수 본문이 없으며 테이블이 단일 SELECT 문의 결과 집합입니다. **[예](https://msdn.microsoft.com/library/bb386954(v=vs.110).aspx)**
  
**시스템 함수**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다양한 작업을 수행하는 데 사용되는 다양한 시스템 함수를 제공합니다. 기본 제공 함수는 수정할 수 없습니다. 자세한 내용은 [기본 제공 함수&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md), [시스템 저장 함수&#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-for-transact-sql.md) 및 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)를 참조하세요.  
  
##  <a name="Guidelines"></a> 지침  
 한 문을 취소하고 모듈(트리거, 저장 프로시저 등)의 다음 문을 실행하도록 하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 오류는 함수 내에서 다르게 처리됩니다. 함수에서 그러한 오류가 발생하면 함수의 실행이 중단됩니다. 이에 따라 함수를 호출한 문도 취소됩니다.  
  
 BEGIN...END 블록 내에 있는 문은 어떠한 부작용도 유발하지 않습니다. 함수의 부작용으로는 데이터베이스 테이블 수정과 같은 함수 외부 범위를 갖는 리소스 상태의 영구적인 변경을 들 수 있습니다. 함수의 문에서 변경할 수 있는 것은 로컬 커서나 변수와 같은 함수의 로컬 개체뿐입니다. 함수에서 수행할 수 없는 동작의 예로는 데이터베이스 테이블의 수정, 함수에서 로컬로 사용되지 않는 커서 작업, 전자 메일 보내기, 카탈로그 수정 시도 및 사용자에게 반환되는 결과 집합 생성 등이 있습니다.  
  
> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 CREATE FUNCTION 문이 실행될 때 존재하지 않는 리소스에 대해 부작용이 생기는 경우에는 이 문을 실행하지만 이 문이 호출되는 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 이 함수가 실행되지 않습니다.  
  
 쿼리에 지정된 함수가 실제로 실행되는 횟수는 최적화 프로그램에서 작성한 실행 계획마다 다릅니다. 예를 들면 WHERE 절의 하위 쿼리에서 호출하는 함수가 있습니다. 하위 쿼리 및 그 함수가 실행되는 횟수는 최적화 프로그램에서 선택한 액세스 경로에 따라 다릅니다.  
  
##  <a name="ValidStatements"></a> 함수의 유효한 문  
함수에서 사용할 수 있는 문의 유형은 다음과 같습니다.  
  
-   함수에서 로컬로 사용되는 데이터 변수와 커서를 정의하는 데 사용되는 DECLARE 문  
  
-   SET을 사용하여 스칼라 및 테이블 지역 변수에 값을 할당하는 것과 같이 함수의 로컬 개체에 값 할당  
  
-   함수에서 커서 선언, 열기, 닫기, 할당 취소 등 로컬 커서를 참조하는 커서 작업. 클라이언트에 데이터를 반환하는 FETCH 문은 사용할 수 없습니다. INTO 절을 사용하여 지역 변수에 값을 할당하는 FETCH 문만 사용할 수 있습니다.  
  
-   TRY...CATCH 문을 제외한 흐름 제어 문  
  
-   함수에서 로컬로 사용되는 변수에 값을 할당하는 식이 있는 선택 목록이 포함된 SELECT 문  
  
-   함수에서 로컬로 사용되는 테이블 변수를 수정하는 UPDATE, INSERT 및 DELETE 문  
  
-   확장 저장 프로시저를 호출하는 EXECUTE 문  
  
### <a name="built-in-system-functions"></a>기본 제공 시스템 함수  
 다음과 같은 비결정적 기본 제공 함수는 Transact-SQL 사용자 정의 함수에 사용할 수 있습니다.  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 다음과 같은 비결정적 기본 제공 함수는 Transact-SQL 사용자 정의 함수에 사용할 수 **없습니다**.  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 결정적 및 비결정적 기본 제공 시스템 함수 목록은 [결정적 함수 및 비결정적 함수](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하세요.  
  
##  <a name="SchemaBound"></a> 스키마 바운드 함수  
 CREATE FUNCTION에서는 테이블, 뷰, 다른 사용자 정의 함수와 같은 참조하는 개체의 스키마에 함수를 바인드하는 SCHEMABINDING 절을 지원합니다. 스키마 바운드 함수에서 참조하는 개체는 변경하거나 삭제할 수 없습니다.  
  
 [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md)에서 SCHEMABINDING 절을 지정하려면 먼저 다음 조건이 만족되어야 합니다.  
  
-   함수에서 참조하는 모든 뷰와 사용자 정의 함수도 스키마 바운드이어야 합니다.  
  
-   함수에서 참조하는 모든 개체가 함수와 같은 데이터베이스에 있어야 합니다. 개체는 한 부분 또는 두 부분으로 된 이름을 사용하여 참조해야 합니다.  
  
-   함수에서 참조하는 모든 개체(테이블, 뷰, 사용자 정의 함수)에 대해 REFERENCES 권한이 있어야 합니다.  
  
 ALTER FUNCTION을 사용하여 스키마 바인딩을 제거할 수 있습니다. ALTER FUNCTION 문에서 WITH SCHEMABINDING 절 없이 함수를 다시 정의해야 합니다.  
  
##  <a name="Parameters"></a> 매개 변수 지정  
 사용자 정의 함수에서는 0이나 더 많은 입력 매개 변수를 사용하고 스칼라 값 또는 테이블을 반환합니다. 하나의 함수에 최대 1024개의 입력 매개 변수를 지정할 수 있습니다. 함수의 매개 변수에 기본값이 지정되면 기본값을 가져오는 함수를 호출할 때 DEFAULT 키워드를 지정해야 합니다. 이 동작은 매개 변수 생략이 기본값을 의미하기도 하는 사용자 정의 저장 프로시저의 기본값이 있는 매개 변수와 다릅니다. 사용자 정의 함수는 출력 매개 변수를 지원하지 않습니다.  
  
##  <a name="Tasks"></a> 추가 예제  
  
|||  
|-|-|  
|**태스크 설명**|**항목**|  
|Transact-SQL 사용자 정의 함수를 만드는 방법에 대해 설명합니다.|[사용자 정의 함수 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|CLR 함수를 만드는 방법에 대해 설명합니다.|[CLR 함수 만들기](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|사용자 정의 집계 함수를 만드는 방법에 대해 설명합니다.|[사용자 정의 집계 만들기](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|Transact-SQL 사용자 정의 함수를 수정하는 방법에 대해 설명합니다.|[사용자 정의 함수 수정](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|사용자 정의 함수를 삭제하는 방법에 대해 설명합니다.|[사용자 정의 함수 삭제](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|사용자 정의 함수를 실행하는 방법에 대해 설명합니다.|[사용자 정의 함수 실행](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|사용자 정의 함수의 이름을 바꾸는 방법에 대해 설명합니다.|[사용자 정의 함수 이름 바꾸기](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|사용자 정의 함수의 정의를 보는 방법에 대해 설명합니다.|[사용자 정의 함수 보기](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  
