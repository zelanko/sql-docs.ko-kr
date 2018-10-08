---
title: '방법: 쿼리를 사용하여 새 데이터베이스 개체 만들기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ac983ac7-f9c4-495d-8a99-e1ba370fb271
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcf7fe3ad0b07b9f8a228318b5eea85b3d8526a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780351"
---
# <a name="how-to-create-new-database-objects-using-queries"></a>방법: 쿼리를 사용하여 새 데이터베이스 개체 만들기
스크립트를 사용하여 뷰, 저장 프로시저, 함수, 트리거, 사용자 정의 형식을 만들거나 편집하려면 Transact\-SQL 편집기를 사용합니다. Transact\-SQL 편집기는 IntelliSense 및 기타 언어 지원을 제공합니다. 자세한 내용은 [Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)을 참조하세요.  
  
Transact\-SQL 편집기는 **코드 보기** 상황에 맞는 메뉴를 사용하여 연결된 데이터베이스 또는 프로젝트의 데이터베이스 엔터티를 열 때 호출됩니다. SQL Server 개체 탐색기의 **새 쿼리** 상황에 맞는 메뉴를 사용하거나 데이터베이스 프로젝트에 새 스크립트 개체를 추가하는 경우에도 이 편집기가 자동으로 열립니다. 데이터베이스에 연결되어 있지 않지만 데이터베이스에 쿼리를 실행하려면 **SQL** 메뉴에서 **Transact-SQL 편집기**를 선택하고 **새 쿼리 연결** 대화 상자를 사용하여 데이터베이스에 연결하고 Transact\-SQL 편집기를 시작할 수 있습니다.  
  
> [!WARNING]  
> 다음 절차에서는 이전의 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에 나오는 절차에서 만든 엔터티를 사용합니다.  
  
### <a name="to-create-a-new-table-using-a-transact-sql-query"></a>Transact\-SQL 쿼리를 사용하여 새 테이블을 만들려면  
  
1.  **Trade** 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
2.  스크립트 창에서 다음 코드를 붙여 넣습니다.  
  
    ```  
  
    CREATE TABLE [dbo].[Fruits] (  
        [Id]         INT NOT NULL,  
        [Perishable] BIT DEFAULT ((1)) NULL,  
        PRIMARY KEY CLUSTERED ([Id] ASC),  
        FOREIGN KEY ([Id]) REFERENCES [dbo].[Products] ([Id])   
    );  
    ```  
  
3.  Transact\-SQL 편집기 도구 모음의 **쿼리 실행** 단추를 클릭하여 이 쿼리를 실행합니다.  
  
4.  **SQL Server 개체 탐색기**에서 **Trade** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다. 새 **Fruits** 테이블이 데이터베이스에 추가되었는지 확인합니다.  
  
### <a name="to-create-a-new-function"></a>새 함수를 만들려면  
  
1.  현재 Transact\-SQL 편집기의 코드를 다음과 같이 바꿉니다.  
  
    ```  
  
    CREATE FUNCTION [dbo].GetProductsBySupplier  
    (  
    @SupplierId int  
    )  
    RETURNS @returntable TABLE   
    (  
    [Id] int NOT NULL,   
    [Name] NVARCHAR (128) NOT NULL,  
    [Shelflife] INT NOT NULL,  
    [SupplierId] INT NOT NULL,  
    [CustomerId] INT NOT NULL  
    )  
    AS  
    BEGIN  
    INSERT @returntable  
    SELECT *  from Products p  
    where p.SupplierId = @SupplierId  
    RETURN   
    END  
    ```  
  
    이 함수는 `Products` 테이블에서 `SupplierId`가 지정된 매개 변수와 같은 행을 모두 반환합니다. Transact\-SQL 편집기 도구 모음의 **쿼리 실행** 단추를 클릭하여 이 쿼리를 실행합니다.  
  
2.  SQL Server 개체 탐색기의 **Trade** 노드에서 **프로그래밍 기능** 및 **함수** 노드를 확장합니다. **테이블 반환 함수** 아래에서 방금 만든 새 함수를 볼 수 있습니다.  
  
### <a name="to-create-a-new-view"></a>새 뷰를 만들려면  
  
1.  현재 Transact\-SQL 편집기의 코드를 다음과 같이 바꿉니다. 그런 다음, 편집기 위의 **쿼리 실행** 단추를 클릭하여 이 쿼리를 실행합니다.  
  
    ```  
    CREATE VIEW [dbo].PerishableFruits   
    AS SELECT p.Id, p.Name FROM dbo.Products p  
    join dbo.Fruits f on f.Id = p.Id  
    where f.Perishable = 1  
    ```  
  
2.  SQL Server 개체 탐색기의 **Trade** 노드에서 **뷰** 노드를 확장하여 방금 만든 새 뷰를 찾습니다.  
  
## <a name="see-also"></a>참고 항목  
[테이블 및 관계 관리, 오류 해결](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[Transact-SQL 편집기를 사용하여 스크립트 편집 및 실행](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
