---
title: 고유하게 컴파일된 T-SQL 모듈 변경 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03f7e4fd87068e31674e74dc81dd33dadba323cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951262"
---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]) 및 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 `ALTER` 문을 사용하여 고유하게 컴파일된 저장 프로시저와 스칼라 UDF, 트리거 등 고유하게 컴파일된 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈에 대해 `ALTER` 작업을 수행할 수 있습니다.  
  
고유하게 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈에 대해 `ALTER`를 실행하면 새 정의를 사용하여 모듈이 다시 컴파일됩니다. 다시 컴파일이 진행되는 동안에는 이전 버전의 모듈을 계속 실행할 수 있습니다. 컴파일이 완료되면 모듈 실행이 종료되고 새 버전의 모듈이 설치됩니다. 고유하게 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈을 변경하는 경우 다음 옵션을 수정할 수 있습니다.  
  
-   매개 변수  
-   EXECUTE AS  
-   TRANSACTION ISOLATION LEVEL  
-   LANGUAGE  
-   DATEFIRST  
-   DATEFORMAT  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
> 고유하게 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈을 고유하게 컴파일되지 않은 모듈로 변환할 수는 없습니다. 고유하게 컴파일되지 않은 T-SQL 모듈을 고유하게 컴파일된 모듈로 변환할 수는 없습니다.  
  
`ALTER PROCEDURE` 기능과 구문에 대한 자세한 내용은 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)를 참조하세요.  
  
고유하게 컴파일된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈에서 [sp_recompile](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)을 실행할 수 있으며 다음 실행 시 모듈이 다시 컴파일됩니다.  
  
## <a name="example"></a>예제  
다음 예에서는 메모리 최적화 테이블(T1)과 T1의 모든 열을 선택하는 고유하게 컴파일된 저장 프로시저(usp_1)를 만듭니다. 그런 다음, `EXECUTE AS` 절을 제거하고, `LANGUAGE`를 변경하고, T1에서 하나의 열(C1)만 선택하도록 usp_1을 변경합니다.  
  
```sql  
CREATE TABLE [dbo].[T1] (  
  [c1] [int] NOT NULL,  
  [c2] [float] NOT NULL,  
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
   SELECT c1, c2 FROM dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
   SELECT c1 FROM dbo.T1  
END  
GO    
```   
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)    
