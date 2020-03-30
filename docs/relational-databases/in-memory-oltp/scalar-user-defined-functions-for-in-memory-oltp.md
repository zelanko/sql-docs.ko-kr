---
title: 메모리 내 OLTP에 대한 사용자 정의 스칼라 함수 | Microsoft 문서
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d2546e40-fdfc-414b-8196-76ed1f124bf5
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3614b1f9c058405c041aa2b4de27d97caadb8fd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68111760"
---
# <a name="scalar-user-defined-functions-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 사용자 정의 스칼라 함수
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서는 고유하게 컴파일된 사용자 정의 스칼라 함수를 생성 및 삭제할 수 있습니다. 또한, 이러한 사용자 정의 함수를 변경하는 것도 가능합니다. 네이티브 컴파일을 사용하면 Transact-SQL에서 사용자 정의 함수의 평가 성능을 향상할 수 있습니다.  
  
 고유하게 컴파일된 사용자 정의 스칼라 함수를 변경하는 경우 작업은 계속 실행되고 함수의 새 버전이 컴파일되는 반면 애플리케이션을 계속 사용할 수 있습니다.  
  
 지원되는 T-SQL 구문에 대한 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.  
  
## <a name="creating-dropping-and-altering-user-defined-functions"></a>사용자 정의 함수 생성, 제거 및 변경  
 CREATE FUNCTION을 사용하여 고유하게 컴파일된 사용자 정의 스칼라 함수를 만들고 DROP FUNCTION을 사용하여 사용자 정의 함수를 삭제하며 ALTER FUNCTION를 사용하여 함수를 변경합니다. 사용자 정의 함수에서는 BEGIN ATOMIC WITH가 필수입니다.  
  
 지원되는 구문 및 모든 제한 사항에 대한 정보는 다음 항목을 참조하십시오.  
  
-   [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
-   [ALTER FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)  
  
-   [DROP FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)  
  
     고유하게 컴파일된 사용자 정의 스칼라 함수에 대한 DROP FUNCTION 구문은 해석된 사용자 정의 함수와 동일합니다.  
  
-   [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
 [sp_recompile&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) 저장 프로시저는 고유하게 컴파일된 사용자 정의 스칼라 함수에서 사용할 수 있습니다. 이를 통해 메타데이터에 존재하는 정의를 사용하여 함수를 컴파일할 수 있습니다.  
  
 다음 예제는 [AdventureWorks2016CTP3](https://www.microsoft.com/download/details.aspx?id=49502) 예제 데이터베이스의 스칼라 UDF를 보여줍니다.  
  
```sql  
CREATE FUNCTION [dbo].[ufnLeadingZeros_native](@Value int)   
RETURNS varchar(8)   
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS   
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
  
    DECLARE @ReturnValue varchar(8);  
    SET @ReturnValue = CONVERT(varchar(8), @Value);  
       DECLARE @i int = 0, @count int = 8 - LEN(@ReturnValue)  
  
    WHILE @i < @count  
       BEGIN  
            SET @ReturnValue = '0' + @ReturnValue;  
            SET @i += 1  
       END  
  
    RETURN (@ReturnValue);  
  
END  
```  
  
## <a name="calling-user-defined-functions"></a>사용자 정의 함수 호출  
 고유하게 컴파일된 사용자 정의 스칼라 함수는 기본 제공 스칼라 함수 및 해석된 사용자 정의 스칼라 함수의 동일한 위치에 있는 식에서 사용될 수 있습니다. 또한, 고유하게 컴파일된 사용자 정의 스칼라 함수는 Transact-SQL 문 및 고유하게 컴파일된 저장 프로시저에 있는 EXECUTE 문과 함께 사용될 수 있습니다.  
  
 이러한 사용자 정의 스칼라 함수는 고유하게 컴파일된 저장 프로시저 및 고유하게 컴파일된 사용자 정의 함수에서 사용할 수 있고 거기에서는 기본 제공 함수가 허용됩니다. 또한, 고유하게 컴파일된 사용자 정의 스칼라 함수를 기존 Transact-SQL 모듈에서도 사용할 수 있습니다.  
  
 이러한 사용자 정의 스칼라 함수를 interop 모드에서 사용할 수 있고 여기에서는 해석된 사용자 정의 해석 함수도 사용할 수 있습니다. **Transactions with Memory-Optimized Tables** (메모리 액세스에 최적화된 테이블 트랜잭션)의 [크로스 컨테이너 트랜잭션에 대하여 지원되는 격리 수준](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)섹션에서의 설명과 같이 이러한 사용 방법은 크로스 컨테이너 제한 사항에 따라 달라집니다. Interop 모드에 대한 자세한 내용은 [해석된 Transact-SQL을 사용하여 메모리 액세스에 최적화된 테이블에 액세스](../../relational-databases/in-memory-oltp/accessing-memory-optimized-tables-using-interpreted-transact-sql.md)를 참조하세요.  
  
 고유하게 컴파일된 사용자 정의 스칼라 함수에서는 명시적인 실행 컨텍스트가 필요합니다. 자세한 내용은 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)을 참조하세요. EXECUTE AS CALLER는 지원되지 않습니다. 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)을 참조하세요.  
  
 고유하게 컴파일된 사용자 정의 스칼라 함수에서 사용할 수 있는 Transact-SQL Execute 문에서 지원되는 구문은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)을 참조하세요. 고유하게 컴파일된 저장 프로시저에서 사용자 정의 함수를 실행하기 위해 지원되는 구문은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.  
  
## <a name="hints-and-parameters"></a>힌트와 매개 변수  
 고유하게 컴파일된 사용자 정의 스칼라 함수에서의 테이블, 조인 및 쿼리 힌트에 대한 지원은 고유하게 컴파일된 저장 프로시저에 대한 해당 힌트 지원과 동일합니다. 해석된 사용자 정의 해석 함수와 동일하게, 고유하게 컴파일된 사용자 정의 스칼라 함수를 참조하는 TRANSACT-SQL 쿼리에 포함된 쿼리 힌트는 이 사용자 정의 함수에 대한 쿼리 계획에 영향을 주지 않습니다.  
  
 사용자 정의 스칼라 함수에서 매개 변수가 허용되는 한 고유하게 컴파일된 사용자 정의 스칼라 함수에서 지원되는 매개 변수를 고유하게 컴파일된 저장 프로시저에서 지원되는 모든 매개 변수입니다. 지원되는 매개 변수의 예는 테이블 반환 매개 변수입니다.  
  
## <a name="schema-bound"></a>스키마 바운드  
 다음은 고유하게 컴파일된 사용자 정의 스칼라 함수에 적용됩니다.  
  
-   CREATE FUNCTION 및 ALTER FUNCTION에서 WITH SCHEMABINDING 인수를 사용하여 스키마 바운드되어야 합니다.  
  
-   스키마 바운드 저장 프로시저 또는 사용자 정의 함수에 의해 참조되는 경우 삭제하거나 변경할 수 없습니다.  
  
## <a name="showplan_xml"></a>SHOWPLAN_XML  
 고유하게 컴파일된 사용자 정의 스칼라 함수는 SHOWPLAN_XML을 지원합니다. 고유 하 게 컴파일된 저장 프로시저에서와 같이 일반 SHOWPLAN_XML 스키마를 준수합니다. 사용자 정의 함수에 대한 기본 요소는 `<UDF>`입니다.  
  
 STATISTICS XML은 고유하게 컴파일된 사용자 정의 스칼라 함수에서 지원되지 않습니다. STATISTICS XML이 활성화된 상태에서 사용자 정의 함수를 참조하는 쿼리를 실행하는 경우 사용자 정의 함수에 대한 부분 없이 XML 콘텐츠가 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 고유하게 컴파일된 저장 프로시저에서와 같이, 고유하게 컴파일된 사용자 정의 스칼라 함수에서 참조되는 개체 권한은 함수가 생성될 때 확인됩니다. 가장된 사용자가 올바른 권한을 가지고 있지 않은 경우 CREATE FUNCTION이 실패합니다. 권한이 변경되어 가장된 사용자가 올바른 권한을 더 이상 갖지 못하는 경우 이후의 사용자 정의 함수 실행이 실패합니다.  
  
 고유하게 컴파일된 저장 프로시저에서 고유하게 컴파일된 사용자 정의 스칼라 함수를 사용하는 경우 외부 프로시저가 생성될 때 사용자 정의 함수 실행 권한이 확인됩니다. 외부 프로시저에 의해 가장된 사용자가 사용자 정의 함수에 대한 EXEC 권한을 가지고 있지 않으면 저장 프로시저 생성이 실패합니다. 사용 권한이 변경되어 사용자가 EXEC 권한을 더 이상 갖지 않으면 외부 프로시저 실행이 실패합니다.  
  
## <a name="see-also"></a>참고 항목  
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [XML 형식으로 실행 계획 저장](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
