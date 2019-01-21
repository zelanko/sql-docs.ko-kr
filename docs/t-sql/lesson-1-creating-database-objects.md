---
title: 'T-SQL 자습서: 데이터베이스 개체 만들기 및 쿼리 | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 9fb8656b-0e4e-4ada-b404-4db4d3eea995
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7887e63dbe7879a17433dce0bd35c346c860097e
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299290"
---
# <a name="lesson-1-create-and-query-database-objects"></a>1단원: 데이터베이스 개체 만들기 및 쿼리
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

  > [!div class="nextstepaction"]
  > [SQL Docs 목차에 대한 피드백을 공유하세요!](https://aka.ms/sqldocsurvey)

이 단원에서는 데이터베이스를 만들고 데이터베이스에서 테이블을 만든 다음 테이블의 데이터에 액세스 및 변경하는 방법에 대해 보여 줍니다. 이 단원은 [!INCLUDE[tsql](../includes/tsql-md.md)]사용을 소개하는 데 목적이 있으므로 이러한 문에 사용 가능한 많은 옵션을 사용하거나 설명하지는 않습니다.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] 문을 다음과 같은 방법으로 작성하여 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에 제출할 수 있습니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]사용. 이 자습서에서는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]를 사용한다고 가정하지만 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Microsoft 다운로드 센터 [에서 무료로 다운로드할 수 있는](https://go.microsoft.com/fwlink/?linkid=67359)Express를 사용할 수도 있습니다.  
  
-   [sqlcmd 유틸리티](../tools/sqlcmd-utility.md)사용  
  
-   만드는 애플리케이션에서 연결  
  
코드 문을 전송하는 방법에 상관없이 코드는 동일한 방법과 동일한 사용 권한으로 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 실행됩니다.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] 에서 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]문을 실행하려면 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 를 열고 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]인스턴스에 연결합니다.  

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.

SQL Server 인스턴스에 대한 액세스 권한이 없는 경우 다음 링크에서 플랫폼을 선택합니다. SQL 인증을 선택한 경우 SQL Server 로그인 자격 증명을 사용합니다.
- **Windows**: [SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="create-a-database"></a>데이터베이스 만들기
많은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문과 마찬가지로 CREATE DATABASE 문에는 필수 매개 변수로 데이터베이스 이름이 있습니다. 또한 CREATE DATABASE에는 데이터베이스 파일을 저장할 디스크 위치와 같은 많은 선택적 매개 변수가 있습니다. 선택적 매개 변수 없이 CREATE DATABASE를 실행할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 이러한 여러 매개 변수에 기본값을 사용합니다. 이 자습서에서는 아주 약간의 선택적 구문 매개 변수만 사용합니다.   

1.  쿼리 편집기 창에서 다음 코드를 입력하되 실행하지는 않습니다.  
  
    ```sql  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  포인터를 사용하여 `CREATE DATABASE`단어를 선택한 다음 **F1**키를 누릅니다. SQL Server 온라인 설명서의 CREATE DATABASE 항목이 열립니다. 이 기술을 사용하여 CREATE DATABASE 및 이 자습서에 사용되는 다른 문의 전체 구문을 찾을 수 있습니다.  
  
3.  쿼리 편집기에서 **F5** 키를 눌러 문을 실행하고 `TestData`라는 데이터베이스를 만듭니다.  
  
데이터베이스를 만들 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 **model** 데이터베이스의 복사본을 만들고 복사본의 이름을 데이터베이스 이름으로 바꿉니다. 선택적 매개 변수로 데이터베이스의 처음 크기를 큰 값으로 지정하지 않은 경우 이 작업은 몇 초 내에 수행되어야 합니다.  
  
> [!NOTE]  
> 단일 일괄 처리에서 둘 이상의 문을 전송할 경우 GO 키워드는 문을 구분합니다. 일괄 처리에 문이 하나만 포함된 경우 GO는 선택 사항입니다.  

## <a name="create-a-table"></a>테이블 만들기
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

테이블을 만들려면 테이블의 이름과 테이블에 있는 각 열의 이름 및 데이터 형식을 제공해야 합니다. 또한 각 열에서 Null 값이 허용되는지 여부를 나타내는 것이 좋습니다. 테이블을 만들려면 테이블이 포함될 스키마에 대한 `CREATE TABLE` 권한 및 `ALTER SCHEMA` 권한이 있어야 합니다. [`db_ddladmin`](../relational-databases/security/authentication-access/database-level-roles.md) 고정 데이터베이스 역할에는 이러한 사용 권한이 있습니다.  
  
대부분의 테이블에는 하나 이상의 테이블 열로 구성되는 기본 키가 있습니다. 기본 키는 항상 고유합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서는 기본 키 값을 테이블에서 반복할 수 없다는 제한이 적용됩니다.  
  
데이터 형식 목록과 각 형식에 대한 설명 링크를 보려면 [데이터 형식&#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)]을 대/소문자를 구분하거나 구분하지 않도록 설치할 수 있습니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 대/소문자를 구분하도록 설치할 경우 개체 이름은 항상 대/소문자가 동일해야 합니다. 예를 들면 OrderData 테이블은 ORDERDATA 테이블과 다릅니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 대/소문자를 구분하지 않도록 설치할 경우 이러한 두 테이블 이름은 같은 것으로 간주되므로 해당 이름을 한 번만 사용할 수 있습니다.  
  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>쿼리 편집기 연결을 TestData 데이터베이스로 전환  
쿼리 편집기 창에서 다음 코드를 입력하고 실행하여 연결을 `TestData` 데이터베이스로 변경합니다.  
  
  ```sql  
  USE TestData  
  GO  
  ```  
  
### <a name="create-the-table"></a>테이블 만들기
쿼리 편집기 창에서 다음 코드를 입력하고 실행하여 `Products`라는 간단한 테이블을 만듭니다. 이 테이블에 있는 열의 이름은 `ProductID`, `ProductName`, `Price`및 `ProductDescription`입니다. `ProductID` 열은 테이블의 기본 키입니다. `int`, `varchar(25)`, `money`및 `text` 는 모두 데이터 형식입니다. 행을 삽입하거나 변경할 경우 `Price` 및 `ProductionDescription` 열만 데이터를 가질 수 없습니다. 이 문에는 스키마라고 하는 선택적 요소(`dbo.`)가 포함되어 있습니다. 스키마는 테이블을 소유하는 데이터베이스 개체입니다. 관리자의 경우에 기본 스키마는 `dbo` 입니다. `dbo` 는 데이터베이스 소유자를 나타냅니다.  
  
  ```sql  
  CREATE TABLE dbo.Products  
     (ProductID int PRIMARY KEY NOT NULL,  
     ProductName varchar(25) NOT NULL,  
     Price money NULL,  
     ProductDescription text NULL)  
  GO  
 ```  

## <a name="insert-and-update-data-in-a-table"></a>테이블에서 데이터 삽입 및 업데이트
이제 **Products** 테이블을 만들었으므로 INSERT 문을 사용하여 테이블에 데이터를 삽입할 준비가 되었습니다. 데이터가 삽입된 후 UPDATE 문을 사용하여 행 내용을 변경합니다. UPDATE 문의 WHERE 절을 사용하여 업데이트를 단일 행으로 제한합니다. 4개의 문이 다음 데이터를 입력합니다.  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3.17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|.52||  
  
기본 구문은 다음과 같습니다. INSERT, 테이블 이름, 열 목록, VALUES, 삽입할 값 목록을 차례로 포함합니다. 줄의 맨 앞에 있는 두 개의 하이픈은 해당 줄이 주석이며 컴파일러에서 텍스트를 무시한다는 것을 나타냅니다. 이 경우에는 허용되는 구문 변형을 주석에서 설명합니다.  
  
### <a name="insert-data-into-a-table"></a>데이터를 테이블에 삽입  
  
1.  다음 문을 실행하여 이전 태스크에서 만든 `Products` 테이블에 행을 삽입합니다. 기본 구문은 다음과 같습니다.  
  
   ```sql 
   -- Standard syntax  
   INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
       VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
   GO   
   ```  
  
2.  다음 문은 필드 목록(괄호로 묶인 부분) 및 값 목록에서 `ProductID` 및 `ProductName` 의 위치를 전환하여 매개 변수가 제공되는 순서를 변경하는 방법을 보여 줍니다.  
  
   ```sql  
   -- Changing the order of the columns  
   INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
       VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
   GO    
   ```  
  
3.  다음 문은 값이 올바른 순서로 나열되는 경우 열 이름이 선택 사항임을 보여 줍니다. 이 구문이 일반적이기는 하지만 다른 사람이 코드를 이해하기 어려울 수 있으므로 이 구문을 사용하지 않는 것이 좋습니다. `NULL` 이 `Price` 열에 대해 지정되는데, 이 제품의 가격을 아직 알 수 없기 때문입니다.  
  
   ```sql  
   -- Skipping the column list, but keeping the values in order  
   INSERT dbo.Products  
       VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
   GO  
  ```  
  
4.  기본 스키마에서 테이블을 액세스 및 변경하는 경우 스키마 이름은 선택 사항입니다. `ProductDescription` 열에서 Null 값을 허용하고 제공되는 값이 없으므로 `ProductDescription` 열 이름과 값을 문에서 완전히 삭제할 수 있습니다.  
  
   ```sql  
   -- Dropping the optional dbo and dropping the ProductDescription column  
   INSERT Products (ProductID, ProductName, Price)  
       VALUES (3000, '3mm Bracket', .52)  
   GO  
   ```  
  
### <a name="update-the-products-table"></a>상품 테이블 업데이트  
다음 `UPDATE` 문을 입력하고 실행하여 두 번째 제품의 `ProductName` 을 `Screwdriver`에서 `Flat Head Screwdriver`로 변경합니다.  
  
  ```sql  
  UPDATE dbo.Products  
      SET ProductName = 'Flat Head Screwdriver'  
      WHERE ProductID = 50  
  GO  
  ```  

## <a name="read-data-from-a-table"></a>테이블의 데이터 읽기
SELECT 문을 사용하여 테이블의 데이터를 읽을 수 있습니다. SELECT 문은 가장 중요한 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 중 하나이며 구문은 다양하게 변형되어 사용됩니다. 이 자습서에서는 5개의 간단한 버전을 사용합니다.  
  
### <a name="read-the-data-in-a-table"></a>테이블에서 데이터 읽기  
  
1.  다음 문을 입력하고 실행하여 `Products` 테이블의 데이터를 읽습니다.  
  
  ```sql 
  -- The basic syntax for reading data from a single table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
  GO  
  ```  
  
2.  별표를 사용하여 테이블의 모든 열을 선택할 수 있습니다. 이 방법은 임시 쿼리에서 사용되는 경우가 많습니다. 나중에 새 열이 테이블에 추가되는 경우에도 문에서 예측된 열을 반환하도록 영구 코드로 열 목록을 제공해야 합니다.  
  
  ```sql  
  -- Returns all columns in the table  
  -- Does not use the optional schema, dbo  
  SELECT * FROM Products  
  GO   
  ```  
  
3.  반환하지 않으려는 열은 생략할 수 있습니다. 열은 나열된 순서대로 반환됩니다.  
  
  ```sql  
  -- Returns only two of the columns from the table  
  SELECT ProductName, Price  
      FROM dbo.Products  
  GO    
  ```  
  
4.  `WHERE` 절을 사용하여 사용자에게 반환되는 행을 제한할 수 있습니다.  
  
  ``` sql 
  -- Returns only two of the records in the table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
      WHERE ProductID < 60  
  GO    
  ```  
  
5.  열이 반환되면 열의 값에 대한 작업을 수행할 수 있습니다. 다음 예는 `Price` 열에서 수치 연산을 수행합니다. `AS` 키워드를 사용하여 이름을 제공하지 않은 경우 이 방법으로 변경된 열에는 이름이 없습니다.  
  
  ```sql  
  -- Returns ProductName and the Price including a 7% tax  
  -- Provides the name CustomerPays for the calculated column  
  SELECT ProductName, Price * 1.07 AS CustomerPays  
      FROM dbo.Products  
  GO  
  ```  
  
### <a name="useful-functions-in-a-select-statement"></a>SELECT 문의 유용한 함수  
SELECT 문에서 데이터 작업을 수행하는 데 사용할 수 있는 일부 함수에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
|||  
|-|-|  
|[문자열 함수&#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[수치 연산 함수&#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[텍스트 및 이미지 함수&#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  

## <a name="create-views-and-stored-procedures"></a>보기 및 저장 프로시저 만들기
뷰는 저장된 SELECT 문이며 저장 프로시저는 일괄 처리로 실행되는 하나 이상의 [!INCLUDE[tsql](../includes/tsql-md.md)] 문입니다.  
  
뷰는 테이블처럼 쿼리되며 매개 변수를 허용하지 않습니다. 저장 프로시저는 뷰보다 복잡합니다. 저장 프로시저는 입력 및 출력 매개 변수를 가질 수 있으며 코드 흐름을 제어하기 위해 IF 및 WHILE 문과 같은 문을 포함할 수 있습니다. 데이터베이스의 모든 반복되는 동작에 저장 프로시저를 사용하는 것이 바람직한 프로그래밍 방식입니다.  
  
예를 들어 CREATE VIEW를 사용하여 **Products** 테이블에 있는 두 개의 열만 선택하는 뷰를 만듭니다. 그런 다음 CREATE PROCEDURE를 사용하여 가격 매개 변수를 허용하고 지정된 매개 변수 값보다 가격이 낮은 제품만 반환하는 저장 프로시저를 만듭니다.  
  
### <a name="create-a-view"></a>보기 만들기  
  
다음 문을 실행하여 select 문을 실행하고 제품의 이름과 가격을 사용자에게 반환하는 매우 간단한 뷰를 만듭니다.  
  
  ```sql  
  CREATE VIEW vw_Names  
     AS  
     SELECT ProductName, Price FROM Products;  
  GO    
  ```  
  
### <a name="test-the-view"></a>뷰 테스트  
  
뷰는 테이블처럼 처리됩니다. `SELECT` 문을 사용하여 뷰에 액세스할 수 있습니다.  
  
  ```sql  
  SELECT * FROM vw_Names;  
  GO   
  ```  
  
### <a name="create-a-stored-procedure"></a>저장 프로시저 만들기  
  
다음 문은 저장 프로시저 이름인 `pr_Names`를 만들고 `@VarPrice` 데이터 형식의 `money`라는 입력 매개 변수를 허용합니다. 이 저장 프로시저는 `Products less than` 데이터 형식에서 `money` 문자 데이터 형식으로 변경되는 입력 매개 변수와 연결된 `varchar(10)` 문을 인쇄합니다. 그런 다음 이 저장 프로시저는 입력 매개 변수를 `SELECT` 절의 일부로 전달하며 뷰에서 `WHERE` 문을 실행합니다. 이렇게 하면 입력 매개 변수 값보다 가격이 낮은 모든 제품이 반환됩니다.  
  
  ```sql  
  CREATE PROCEDURE pr_Names @VarPrice money  
     AS  
     BEGIN  
        -- The print statement returns text to the user  
        PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
        -- A second statement starts here  
        SELECT ProductName, Price FROM vw_Names  
              WHERE Price < @varPrice;  
     END  
  GO    
  ```  
  
### <a name="test-the-stored-procedure"></a>저장 프로시저 테스트  
  
저장 프로시저를 테스트하려면 다음 문을 입력하고 실행합니다. 이 프로시저는 1단원에서 가격이 `Products` 보다 낮은 `10.00`테이블에 입력한 제품 두 개의 이름을 반환해야 합니다.  
  
  ```sql  
  EXECUTE pr_Names 10.00;  
  GO  
  ```  

## <a name="next-steps"></a>다음 단계
다음 아티클에서는 데이터베이스 개체에서 사용 권한을 구성하는 방법을 설명합니다. 1단원에서 만든 개체도 2단원에서 사용합니다. 

자세히 알아보려면 다음 문서로 이동합니다.
> [!div class="nextstepaction"]
> [다음 단계](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
  
