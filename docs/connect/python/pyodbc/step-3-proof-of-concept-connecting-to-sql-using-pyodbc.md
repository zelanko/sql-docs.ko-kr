---
title: '3단계: pyodbc를 사용하여 SQL에 연결하는 개념 증명 | Microsoft Docs'
ms.custom: ''
ms.date: 10/09/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e241d84ebc60acceafe09b1a9240711a72d2067
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798322"
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
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>3 단계: 행 삽입  
  
이 예제에서는 [INSERT](../../../t-sql/statements/insert-transact-sql.md) 명령문을 안전하게 실행하고 [SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값으로부터 애플리케이션을 보호하는 매개 변수를 전달하는 방법을 보여줍니다.    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-aad-and-the-connection-string"></a>AAD (Azure Active Directory) 및 연결 문자열

pyODBC가 SQL Server용 Microsoft ODBC 드라이버를 사용합니다.
ODBC 드라이버의 버전이 17.1 이상인 경우 pyODBC를 통해 ODBC 드라이버의 AAD 대화형 모드를 사용할 수 있습니다.
이 AAD 대화형 옵션은 Python 및 pyODBC에서 ODBC 드라이버가 대화 상자를 표시할 수 있도록 허용 하는 경우 작동 합니다.
이 옵션은 Windows 운영 체제 에서만 사용할 수 있습니다.

### <a name="example-connection-string-for-aad-interactive-authentication"></a>AAD 대화형 인증에 대 한 연결 문자열 예

다음은 AAD 대화형 인증을 지정 하는 ODBC 연결 문자열의 예입니다.

- `server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

ODBC 드라이버의 AAD 인증 옵션에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [ODBC 드라이버에서 Azure Active Directory 사용](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)

## <a name="next-steps"></a>다음 단계
  
자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조 하세요.
