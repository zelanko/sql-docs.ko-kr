---
title: 테이블 만들기(자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 2d4b110446ae27335f65e83958a1a153350ccbcb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62704566"
---
# <a name="creating-a-table-tutorial"></a>테이블 만들기(자습서)
  테이블을 만들려면 테이블의 이름과 테이블에 있는 각 열의 이름 및 데이터 형식을 제공해야 합니다. 또한 각 열에서 Null 값이 허용되는지 여부를 나타내는 것이 좋습니다.  
  
 대부분의 테이블에는 하나 이상의 테이블 열로 구성되는 기본 키가 있습니다. 기본 키는 항상 고유합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서는 기본 키 값을 테이블에서 반복할 수 없다는 제한이 적용됩니다.  
  
 데이터 형식 목록과 각 형식에 대한 설명 링크를 보려면 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../includes/ssde-md.md)]을 대/소문자를 구분하거나 구분하지 않도록 설치할 수 있습니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 대/소문자를 구분하도록 설치할 경우 개체 이름은 항상 대/소문자가 동일해야 합니다. 예를 들면 OrderData 테이블은 ORDERDATA 테이블과 다릅니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 을 대/소문자를 구분하지 않도록 설치할 경우 이러한 두 테이블 이름은 같은 것으로 간주되므로 해당 이름을 한 번만 사용할 수 있습니다.  
  
### <a name="to-create-a-database-to-contain-the-new-table"></a>새 테이블을 포함하도록 데이터베이스를 만들려면  
  
-   다음 코드를 쿼리 편집기 창에 입력합니다.  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>쿼리 편집기 연결을 TestData 데이터베이스로 전환  
  
-   쿼리 편집기 창에서 다음 코드를 입력하고 실행하여 연결을 `TestData` 데이터베이스로 변경합니다.  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### <a name="to-create-a-table"></a>테이블 형식 보고서를 만들려면  
  
-   쿼리 편집기 창에서 다음 코드를 입력하고 실행하여 `Products`라는 간단한 테이블을 만듭니다. 이 테이블에 있는 열의 이름은 `ProductID`, `ProductName`, `Price`및 `ProductDescription`입니다. `ProductID` 열은 테이블의 기본 키입니다. `int`, `varchar(25)`, `money`및 `text` 는 모두 데이터 형식입니다. 행을 삽입하거나 변경할 경우 `Price` 및 `ProductionDescription` 열만 데이터를 가질 수 없습니다. 이 문에는 스키마라고 하는 선택적 요소(`dbo.`)가 포함되어 있습니다. 스키마는 테이블을 소유하는 데이터베이스 개체입니다. 관리자의 경우에 기본 스키마는 `dbo` 입니다. `dbo` 는 데이터베이스 소유자를 나타냅니다.  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [테이블에서 데이터 삽입 및 업데이트&#40;자습서&#41;](../t-sql/lesson-1-3-inserting-and-updating-data-in-a-table.md)  
  
## <a name="see-also"></a>관련 항목  
 [CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)  
  
  
