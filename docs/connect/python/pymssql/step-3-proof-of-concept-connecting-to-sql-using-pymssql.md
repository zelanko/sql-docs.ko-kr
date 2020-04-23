---
title: '3단계: pymssql를 사용하여 SQL에 연결'
description: 3단계는 Python 및 pymssql을 사용하여 SQL Server에 연결할 수 있는 방법을 보여 주는 개념 증명입니다. 기본 예제에서는 데이터를 선택하고 삽입하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1c75d13e9e44632c411639385227776f54ca1a9
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528567"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>3단계: pymssql을 사용하여 SQL에 연결하는 개념 증명
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

이 예제는 개념 증명으로만 간주해야 합니다.  이 샘플 코드는 명확하게 하기 위해 단순화되었으며 반드시 Microsoft에서 권장하는 모범 사례를 대표하지는 않습니다.  
  
## <a name="step-1--connect"></a>1단계:  연결  
  
SQL Database에 연결하는 데 [pymssql.connect](https://pypi.org/project/pymssql/) 함수가 사용됩니다.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>2단계:  쿼리 실행  
  
[cursor.execute](https://pypi.org/project/pymssql/) 함수를 사용하여 SQL Database에 대한 쿼리에서 결과 집합을 검색할 수 있습니다. 이 함수는 본질적으로 모든 쿼리를 허용하며, [cursor.fetchone()](https://pypi.org/project/pymssql/)을 사용하여 반복될 수 있는 결과 집합을 반환합니다.  
  
  
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
  
## <a name="step-3--insert-a-row"></a>3단계:  행 삽입  
  
이 예에서는 [INSERT](../../../t-sql/statements/insert-transact-sql.md) 문을 안전하게 실행하고 매개 변수를 전달하는 방법을 확인합니다. 매개 변수를 값으로 전달하면 [SQL 삽입](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)으로부터 애플리케이션이 보호됩니다.  
  
  
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
  
## <a name="step-4-roll-back-a-transaction"></a>4단계: 트랜잭션 롤백  
  
이 코드 예제는 다음과 같은 트랜잭션의 사용법을 보여줍니다.  
  
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
  
자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조하세요.
