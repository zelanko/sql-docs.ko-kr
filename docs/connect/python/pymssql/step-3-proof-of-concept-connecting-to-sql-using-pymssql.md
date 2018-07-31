---
title: '3단계: pymssql을 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ea4fa2527fa39700647832bdd1a194389cb36e4
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982235"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>3단계: pymssql을 사용하여 SQL에 연결하는 개념 증명
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

이 예제에서는 개념만 고려 되어야 합니다.  샘플 코드를 이해 하기 쉽도록 간소화 되었습니다 및 Microsoft에서 권장 하는 모범 사례를 반드시 나타내지는지 않습니다.  
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
합니다 [pymssql.connect](http://pymssql.org/en/latest/ref/pymssql.html) 함수는 SQL Database에 연결 하는 데 사용 됩니다.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>2 단계: 쿼리를 실행 합니다.  
  
합니다 [cursor.execute](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) 결과 SQL Database에 대해 쿼리에서 집합을 검색 하는 함수를 사용할 수 있습니다. 이 함수에서 기본적으로 모든 쿼리를 허용 하 고 사용 하 여 반복 될 수 있는 결과 집합을 반환 합니다 [cursor.fetchone ()](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)합니다.  
  
  
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
  
## <a name="step-3--insert-a-row"></a>3 단계: 행 삽입  
  
이 예제에서는 실행 하는 방법에에서는 [삽입](../../../t-sql/statements/insert-transact-sql.md) 에서 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 전달 하는 문을 [SQL 주입](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값입니다.    
  
  
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
  
* 트랜잭션 시작  
* 데이터 행 삽입  
* 롤백 트랜잭션이 삽입 취소  
  
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
  
자세한 내용은 참조는 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)합니다.
