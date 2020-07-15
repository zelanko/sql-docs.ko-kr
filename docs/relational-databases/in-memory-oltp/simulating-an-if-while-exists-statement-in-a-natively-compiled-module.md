---
title: IF-WHILE EXISTS 시뮬레이션 - 고유하게 컴파일된 모듈
description: SQL Server에서 고유하게 컴파일된 저장 프로시저가 지원하지 않는 조건문에서 EXISTS 절을 시뮬레이트하는 방법을 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f62b799a124eb7ed47ffad9e63d0433172984c18
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735018"
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  고유하게 컴파일된 저장 프로시저는 IF 및 WHILE 절과 같은 조건문에서 **EXISTS** 을 지원하지 않습니다.  
  
 다음 예제에서는 EXISTS 절을 시뮬레이션하도록 SELECT 문으로 BIT 변수를 사용하여 문제를 해결하는 방법을 보여줍니다.  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
