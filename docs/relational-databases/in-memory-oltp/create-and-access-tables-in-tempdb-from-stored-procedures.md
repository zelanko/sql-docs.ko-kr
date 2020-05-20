---
title: 저장 프로시저에서 tempdb 테이블 만들기 및 액세스
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f4ae543590e5985904e44235da89069c06c649ee
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412724"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>저장 프로시저에서 TempDB에 테이블 만들기 및 액세스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  고유하게 컴파일된 저장 프로시저의 TempDB에서 테이블을 만들거나 액세스하는 것은 지원되지 않습니다. 대신, DURABILITY=SCHEMA_ONLY인 메모리 최적화 테이블을 사용하거나 테이블 형식 및 테이블 변수를 사용합니다. 

임시 테이블 및 테이블 변수 시나리오의 메모리 최적화에 대한 자세한 내용은 [메모리 최적화를 사용하여 임시 테이블 및 테이블 변수 성능 향상](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)을 참조하세요.
  
  다음 예제에서는 세 개의 열(id, ProductID, Quantity)로 임시 테이블 사용을 **dbo.OrderQuantityByProduct** 형식의 **\@OrderQuantityByProduct** 테이블 변수를 사용하여 변경할 수 있는 방법을 보여 줍니다.  
  
```sql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
