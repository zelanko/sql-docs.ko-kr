---
title: '3단계: pymssql을 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b56a20a0456bef04553c614432bde270d8e98d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935771"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>3단계: pymssql을 사용하여 SQL에 연결하는 개념 증명
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

이 예는 개념 증명 으로만 간주 해야 합니다.  이 샘플 코드는 명확 하 게 하기 위해 단순화 되었으며 Microsoft에서 권장 하는 모범 사례를 나타내지는 않습니다.  
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
[Pymssql](https://pymssql.org/en/latest/ref/pymssql.html) 함수는 SQL Database에 연결 하는 데 사용 됩니다.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>2 단계: 쿼리 실행  
  
[커서. execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) 함수를 사용 하 여 SQL Database에 대 한 쿼리에서 결과 집합을 검색할 수 있습니다. 이 함수는 기본적으로 모든 쿼리를 허용 하 고 커서를 사용 하 여 반복 될 수 있는 결과 집합을 반환 합니다 [. fetchone ()](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
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
  
이 예제에서는 [SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) [삽입](../../../t-sql/statements/insert-transact-sql.md) 값 으로부터 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 실행 하는 방법을 확인 합니다.    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>4 단계: 트랜잭션 롤백  
  
이 코드 예제에서는 다음을 수행 하는 트랜잭션을 사용 하는 방법을 보여 줍니다.  
  
* 트랜잭션 시작  
* 데이터 행 삽입  
* 트랜잭션을 롤백하여 삽입 취소  
  
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
  
자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조 하세요.
