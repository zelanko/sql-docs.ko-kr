---
title: 고유하게 컴파일된 저장 프로시저 만들기 | Microsoft 문서
description: 고유하게 컴파일된 저장 프로시저에 대해서만 지원되는 Transact-SQL 기능을 알아봅니다. SQL Server에서 고유하게 컴파일된 저장 프로시저를 만드는 방법을 확인합니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 398e9dee801465cffd85d3ce65f0e344318b4cf1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481244"
---
# <a name="creating-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저 만들기
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

고유하게 컴파일된 저장 프로시저는 전체 [!INCLUDE[tsql](../../includes/tsql-md.md)] 프로그래밍 기능 및 쿼리 노출 영역을 구현하지 않습니다. 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 고유하게 컴파일된 저장 프로시저 내에서 사용할 수 없습니다. 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.  
  
다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 기능은 고유하게 컴파일된 저장 프로시저에 대해서만 지원됩니다.  
  
-   ATOMIC 블록 자세한 내용은 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)을(를) 참조하십시오.  
  
-   매개 변수 및 변수에 대한 `NOT NULL` 제약 조건입니다. **NULL** 값을 **NOT NULL** 로 선언된 매개 변수 또는 변수에 할당할 수 없습니다. 자세한 내용은 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)을 참조하세요.  
  
    -   `CREATE PROCEDURE dbo.myproc (@myVarchar VARCHAR(32) NOT NULL) AS (...)`  
  
    -   `DECLARE @myVarchar VARCHAR(32) NOT NULL = "Hello"; -- Must initialize to a value.`  
  
    -   `SET @myVarchar = NULL; -- Compiles, but fails during run time.`  
  
-   고유하게 컴파일된 저장 프로시저의 스키마 바인딩  
  
고유하게 컴파일된 저장 프로시저는 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)를 사용하여 만듭니다. 다음 예에서는 메모리 최적화 테이블과 해당 테이블에 행을 삽입하는 데 사용되는 고유하게 컴파일된 저장 프로시저를 보여 줍니다.  
  
```sql  
CREATE TABLE [dbo].[T2] (  
  [c1] [int] NOT NULL, 
  [c2] [datetime] NOT NULL,
  [c3] nvarchar(5) NOT NULL, 
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_2] (@c1 int, @c3 nvarchar(5)) 
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
  DECLARE @c2 datetime = GETDATE();  
  INSERT INTO [dbo].[T2] (c1, c2, c3) values (@c1, @c2, @c3);  
END  
GO  
```  
 
코드 샘플에서 **NATIVE_COMPILATION** 은 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저가 고유하게 컴파일된 저장 프로시저임을 나타냅니다. 다음 옵션이 필요합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**SCHEMABINDING**|고유하게 컴파일된 저장 프로시저는 참조하는 개체의 스키마에 바인딩되어야 합니다. 이는 프로시저에서 참조하는 테이블을 삭제할 수 없음을 의미합니다. 프로시저에서 참조되는 테이블에는 해당 스키마 이름을 포함해야 하며 쿼리에 와일드카드(\*)를 사용할 수 없습니다( `SELECT * from...`을 의미하지 않음). **SCHEMABINDING** 은 이 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 고유하게 컴파일된 저장 프로시저에 대해서만 지원됩니다.|  
|**BEGIN ATOMIC**|고유하게 컴파일된 저장 프로시저의 본문은 단 하나의 ATOMIC 블록으로 구성되어야 합니다. ATOMIC 블록은 저장 프로시저의 원자성 실행을 보장합니다. 프로시저가 활성 트랜잭션의 컨텍스트 외부에서 호출되면 새 트랜잭션을 시작하며 ATOMIC 블록의 끝에서 커밋합니다. 고유하게 컴파일된 저장 프로시저의 ATOMIC 블록에는 다음과 같은 두 가지 필수 옵션이 있습니다.<br /><br /> **TRANSACTION ISOLATION LEVEL** 입니다. 지원되는 격리 수준은 [메모리 액세스에 최적화된 테이블에 대한 트랜잭션 격리 수준](/previous-versions/sql/sql-server-2016/dn133175(v=sql.130)) 을 참조하세요.<br /><br /> **LANGUAGE** 입니다. 저장 프로시저의 언어는 사용 가능한 언어 또는 언어 별칭 중 하나로 설정되어야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
