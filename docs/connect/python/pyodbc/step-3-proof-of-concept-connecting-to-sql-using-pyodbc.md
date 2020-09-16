---
title: '3단계: pyodbc를 사용하여 SQL에 연결'
description: 3단계는 Python 및 pyODBC를 사용하여 SQL Server에 연결할 수 있는 방법을 보여 주는 개념 증명입니다. 기본 예제에서는 데이터를 선택하고 삽입하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26cbdea53547f30a59dc6953d7bf68bddc712164
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807034"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>3단계: pyodbc를 사용하여 SQL에 연결하는 개념 증명

이 예는 개념 증명입니다. 이 샘플 코드는 명확하게 하기 위해 단순화되었으며 반드시 Microsoft에서 권장하는 모범 사례를 대표하지는 않습니다.  

시작하려면 다음 샘플 스크립트를 실행합니다. test.py라는 파일을 만들고 진행하면서 각 코드 조각을 추가합니다. 

```
> python test.py
```
  
## <a name="connect"></a>연결  
  
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
  
  
## <a name="run-query"></a>쿼리 실행  
  
cursor.execute 함수를 사용하여 SQL Database에 대한 쿼리에서 결과 집합을 검색할 수 있습니다. 이 함수는 쿼리를 허용하며, cursor.fetchone()을 사용하여 반복될 수 있는 결과 집합을 반환합니다.
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="insert-a-row"></a>행 삽입  
  
이 예제에서는 [INSERT](../../../t-sql/statements/insert-transact-sql.md) 문을 안전하게 실행하고 매개 변수를 전달하는 방법을 알아봅니다. 이들 매개 변수가 [SQL 삽입](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)으로부터 애플리케이션을 보호합니다.    
  
  
```python
#Sample insert query
cursor.execute("""
INSERT INTO SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) 
VALUES (?,?,?,?,?)""",
'SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP) 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print('Inserted Product key is ' + str(row[0]))
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-and-the-connection-string"></a>Azure Active Directory 및 연결 문자열

pyODBC가 SQL Server용 Microsoft ODBC 드라이버를 사용합니다.
ODBC 드라이버 버전이 17.1 이상인 경우 pyODBC를 통해 ODBC 드라이버의 Azure Active Directory 대화형 모드를 사용할 수 있습니다.
이 대화형 옵션은 Python 및 pyODBC에서 ODBC 드라이버가 대화 상자를 표시할 수 있도록 허용하는 경우 작동합니다. 이 옵션은 Windows 운영 체제에서만 사용할 수 있습니다. 

### <a name="example-connection-string-for-azure-active-directory-interactive-authentication"></a>Azure Active Directory 대화형 인증을 위한 연결 문자열 예

다음 예에서는 Azure Active Directory 대화형 인증을 지정하는 ODBC 연결 문자열을 제공합니다.

`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

ODBC 드라이버의 인증 옵션에 대한 자세한 내용은 [ODBC 드라이버에서 Azure Active Directory 사용](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)을 참조하세요.

## <a name="next-steps"></a>다음 단계
  
자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조하세요.
