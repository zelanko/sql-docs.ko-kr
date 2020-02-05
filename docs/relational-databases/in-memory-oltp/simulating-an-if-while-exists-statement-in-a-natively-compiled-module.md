---
title: IF-WHILE EXISTS 시뮬레이션 - 고유하게 컴파일된 모듈
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
ms.openlocfilehash: e860bbab32549b72048d30caa93f18daa422cc42
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74412600"
---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>IF 시뮬레이션-고유하게 컴파일된 모듈에서 WHILE EXISTS 문
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

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
  
  
