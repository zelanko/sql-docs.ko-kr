---
title: "고유하게 컴파일된 T-SQL 모듈 변경 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4696039c56ebf5f1fd6ea440cd27da84721f35b9
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 및 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에서는 ALTER 문을 사용하여 고유하게 컴파일된 저장 프로시저와 스칼라 UDF, 트리거 등 고유하게 컴파일된 다른 T-SQL 모듈에 대해 ALTER 작업을 수행할 수 있습니다.  
  
 고유하게 컴파일된 T-SQL 모듈에 대해 ALTER을 실행하면 새 정의를 사용하여 모듈이 다시 컴파일됩니다. 다시 컴파일이 진행되는 동안에는 이전 버전의 모듈을 계속 실행할 수 있습니다. 컴파일이 완료되면 모듈 실행이 종료되고 새 버전의 모듈이 설치됩니다. 고유하게 컴파일된 T-SQL 모듈을 변경하는 경우 다음 옵션을 수정할 수 있습니다.  
  
-   매개 변수  
  
-   EXECUTE AS  
  
-   TRANSACTION ISOLATION LEVEL  
  
-   LANGUAGE  
  
-   DATEFIRST  
  
-   DATEFORMAT  
  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
>  고유하게 컴파일된 T-SQL 모듈을 고유하게 컴파일되지 않은 모듈로 변환할 수는 없습니다. 고유하게 컴파일되지 않은 T-SQL 모듈을 고유하게 컴파일된 모듈로 변환할 수는 없습니다.  
  
 ALTER PROCEDURE 기능과 구문에 대한 자세한 내용은 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)를 참조하세요.  
  
 고유하게 컴파일된 T-SQL 모듈에서 sp_recompile을 실행할 수 있으며 다음 실행 시 모듈이 다시 컴파일됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 메모리 액세스에 최적화된 테이블(T1)과 T1의 모든 열을 선택하는 고유하게 컴파일된 저장 프로시저(SP1)를 만듭니다. 그런 다음 EXECUTE AS 절을 제거하고, LANGUAGE를 변경하고, T1에서 하나의 열(C1)만 선택하도록 SP1을 변경합니다.  
  
```  
CREATE TABLE [dbo].[T1]  
(  
[c1] [int] NOT NULL,  
[c2] [float] NOT NULL,  
CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
 SELECT c1, c2 from dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
 SELECT c1 from dbo.T1  
END  
GO  
  
```  
  
  

