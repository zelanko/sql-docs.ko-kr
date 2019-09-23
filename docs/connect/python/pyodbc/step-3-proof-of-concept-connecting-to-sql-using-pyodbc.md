---
title: '3단계: pyodbc를 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 30ba3db5e23d95128aecbb5cc8974faeb6d58d75
ms.sourcegitcommit: 6413b7495313830ad1ae5aefe0c09e8e7a284b07
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016838"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>3단계: pyodbc를 사용하여 SQL에 연결하는 개념 증명

이 예는 개념 증명 으로만 간주 해야 합니다.  이 샘플 코드는 명확 하 게 하기 위해 단순화 되었으며 Microsoft에서 권장 하는 모범 사례를 나타내지는 않습니다.  

**아래 샘플 스크립트 실행**  Test.py 라는 파일을 만들고 각 코드 조각을 이동 하는 동안 추가 합니다. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>1 단계: 연결  
  
```python

import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>2 단계: 쿼리 실행  
  
커서. executefunction을 사용 하 여 SQL Database에 대 한 쿼리에서 결과 집합을 검색할 수 있습니다. 이 함수는 기본적으로 모든 쿼리를 허용 하 고 커서를 사용 하 여 반복 될 수 있는 결과 집합을 반환 합니다. fetchone ()
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>3 단계: 행 삽입  
  
이 예제에서는 [SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) 삽입 값 으로부터 응용 프로그[램을](../../../t-sql/statements/insert-transact-sql.md) 보호 하는 매개 변수를 안전 하 게 실행 하는 방법을 확인 합니다.    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>다음 단계  
  
자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조 하세요.
