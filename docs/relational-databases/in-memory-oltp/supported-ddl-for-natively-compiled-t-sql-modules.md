---
title: "고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 DDL | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e467fa064651938b649f2f8ebc1cb7d698e1b48
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="supported-ddl-for-natively-compiled-t-sql-modules"></a>고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 DDL
  이 항목에는 저장 프로시저, 스칼라 UDF, 인라인 TVF 및 트리거와 같은 고유하게 컴파일된 T-SQL 모듈에 지원되는 DDL 구문을 나열합니다.  
  
 고유하게 컴파일된 T-SQL 모듈의 일부로 사용할 수 있는 기능 및 T-SQL 노출 영역에 대한 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)을 참조하세요.  
  
 지원되지 않는 구문에 대한 정보는 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조하세요.  
  
 다음 항목이 지원됩니다.  
  
-   [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [DROP PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
-   [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
-   [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md) 및 INSERT SELECT 문  
  
-   SCHEMABINDING 및 BEGIN ATOMIC(고유하게 컴파일된 저장 프로시저에 필요함)  
  
     자세한 내용은 [Creating Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)을 참조하세요.  
  
-   NATIVE_COMPILATION  
  
     자세한 내용은 [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)을 참조하세요.  
  
-   매개 변수 및 변수를 NOT NULL로 선언할 수 있습니다(고유하게 컴파일된 모듈에만 사용 가능: 고유하게 컴파일된 저장 프로시저 및 고유하게 컴파일된 스칼라 사용자 정의 함수).  
  
-   테이블 반환 매개 변수  
  
     자세한 내용은 [테이블 반환 매개 변수 사용&#40;데이터베이스 엔진&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)을 참조하세요.  
  
-   EXECUTE AS OWNER, SELF, CALLER 및 사용자  
  
-   테이블 및 프로시저에 대한 GRANT 및 DENY 권한  
  
     자세한 내용은 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md) 및 [DENY 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
