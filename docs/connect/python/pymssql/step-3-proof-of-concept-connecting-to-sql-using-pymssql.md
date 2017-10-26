---
title: "3 단계: pymssql를 사용 하 여 SQL에 연결 하는 개념 증명 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: f230af88796afce17b6858a7e4ac5136a04e9dd3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>3 단계: pymssql를 사용 하 여 SQL에 연결 하는 개념 증명
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

이 예제에서는 개념 증명을 고려 되어야 합니다.  샘플 코드의 명확성을 위해 간소화 되 고 Microsoft에서 권장 모범 사례 나타내지는지 않습니다.  
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
[pymssql.connect](http://pymssql.org/en/latest/ref/pymssql.html) 함수는 SQL 데이터베이스에 연결 하는 데 사용 됩니다.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>2 단계: 쿼리를 실행 합니다.  
  
[cursor.execute](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) 결과 SQL 데이터베이스에 대해 쿼리에서 집합을 검색 하는 함수를 사용할 수 있습니다. 이 함수에서 기본적으로 모든 쿼리를 허용 하 고 사용 하 여 반복 될 수 있는 결과 집합 반환 [cursor.fetchone()](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)합니다.  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>행을 삽입 하는 3 단계:  
  
이 예제를 실행 하는 방법을 표시 됩니다는 [삽입](../../../t-sql/statements/insert-transact-sql.md) 문을에서 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 전달 [SQL 주입](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값입니다.    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>4 단계: Rollback 트랜잭션  
  
이 코드 예제는 트랜잭션의 사용을 보여 줍니다. 있습니다.  
  
* 트랜잭션을 시작합니다  
* 데이터 행을 삽입 합니다.  
* 롤백 트랜잭션이 삽입을 실행 취소 하려면  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>다음 단계  
  
자세한 내용은 참조는 [Python 개발자 센터](https://azure.microsoft.com/en-us/develop/python/)합니다.

