---
title: 메모리 내 OLTP에 대한 Transact-SQL 지원 | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 164da4fb4a50b5a9637652887e6e5173b3bbaf67
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34325324"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>메모리 내 OLTP에 대한 Transact-SQL 지원
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 메모리 내 OLTP를 지원하는 구문 옵션을 포함합니다.  
  
-   [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)(**MEMORY_OPTIMIZED_DATA** 추가됨)  
  
-   [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
-   [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)(**MEMORY_OPTIMIZED_DATA** 추가됨)  
  
-   [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
-   [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
-   [CREATE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
-   [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
    고유하게 컴파일된 저장 프로시저에서 변수를 **NOT NULL**로 선언할 수 있습니다. 일반적인 저장 프로시저에서 수행할 수 없습니다.  
  
 
            **AUTO_UPDATE_STATISTICS** 는 SQL Server 2016으로 시작하여 메모리 최적화 테이블의 경우 **ON** 일 수 있습니다. 자세한 내용은 [sp_autostats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)를 참조하세요.  
  
 [SET STATISTICS XML&#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md) ON은 고유하게 컴파일된 저장 프로시저에서 지원되지 않습니다.  
  
 지원되지 않는 기능에 대한 자세한 내용은 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조하세요.  
  
 고유하게 컴파일된 저장 프로시저에 지원되는 구문에 대한 자세한 내용은 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 기능](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md) 및 [고유하게 컴파일된 T-SQL 모듈에 대해 지원되는 DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에 대해 지원되지 않는 SQL Server 기능](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)   
 [고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
