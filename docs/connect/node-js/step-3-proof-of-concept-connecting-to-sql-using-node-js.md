---
title: "3 단계: Node.js를 사용 하 여 SQL에 연결 하는 개념 증명 | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5d5b41b6-129a-40b1-af8b-7e8fbd4a84bb
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 1d25bbbad2e6506e505125e2aa9de6212298b4b3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-nodejs"></a>3 단계: Node.js를 사용 하 여 SQL에 연결 하는 개념 증명

![아래쪽 화살표-Circled 다운로드](../../ssdt/media/download.png)[Node.js SQL 드라이버를 다운로드 하려면](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

이 예제에서는 개념 증명을 고려 되어야 합니다.  샘플 코드의 명확성을 위해 간소화 되 고 Microsoft에서 권장 모범 사례 나타내지는지 않습니다. 다른 예제 같은 중요 한 기능을 사용 하 여를 Github에서 사용할 수 있습니다.

- [https://github.com/tediousjs/tedious/blob/master/examples/](https://github.com/tediousjs/tedious/blob/master/examples/)
  
## <a name="step-1-connect"></a>1 단계: 연결  
  
**새 연결** 함수는 SQL 데이터베이스에 연결 하는 데 사용 됩니다.  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // If you are on Microsoft Azure, you need this:  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
    // If no error, then good to proceed.  
        console.log("Connected");  
    });  
```  
  
## <a name="step-2--execute-a-query"></a>2 단계: 쿼리를 실행 합니다.  
  
  
모든 SQL 문을 사용 하 여 실행 하는 **새 Request()** 함수입니다. 문은 select 문과 같은 행을 반환 하는 경우 검색할 수 있습니다 있습니다를 사용 하는 **request.on()** 함수입니다. 행이 없는 request.on() 함수 빈 목록을 반환 합니다.  
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // When you connect to Azure SQL Database, you need these next options.  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement();  
    });  
  
    var Request = require('tedious').Request;  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement() {  
        request = new Request("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;", function(err) {  
        if (err) {  
            console.log(err);}  
        });  
        var result = "";  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                result+= column.value + " ";  
              }  
            });  
            console.log(result);  
            result ="";  
        });  
  
        request.on('done', function(rowCount, more) {  
        console.log(rowCount + ' rows returned');  
        });  
        connection.execSql(request);  
    }  
```  
  
## <a name="step-3-insert-a-row"></a>행을 삽입 하는 3 단계:  
  
이 예제를 실행 하는 방법을 표시 됩니다는 [삽입](../../t-sql/statements/insert-transact-sql.md) 문을에서 응용 프로그램을 보호 하는 매개 변수를 안전 하 게 전달 [SQL 주입](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 값입니다.    
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // If you are on Azure SQL Database, you need these next options.  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement1();  
    });  
  
    var Request = require('tedious').Request  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement1() {  
        request = new Request("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES (@Name, @Number, @Cost, @Price, CURRENT_TIMESTAMP);", function(err) {  
         if (err) {  
            console.log(err);}  
        });  
        request.addParameter('Name', TYPES.NVarChar,'SQL Server Express 2014');  
        request.addParameter('Number', TYPES.NVarChar , 'SQLEXPRESS2014');  
        request.addParameter('Cost', TYPES.Int, 11);  
        request.addParameter('Price', TYPES.Int,11);  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                console.log("Product id of inserted item is " + column.value);  
              }  
            });  
        });       
        connection.execSql(request);  
    }  
```  

