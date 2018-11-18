---
title: '방법: 프로젝트에서 Microsoft SQL Server 2012 개체 사용 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9baf122f-cf22-4860-98db-ef782cd972fc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 539eb7ed053ff4f1d41aaa34360cd71772bbfc9c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681091"
---
# <a name="how-to-use-microsoft-sql-server-2012-objects-in-your-project"></a>방법: 프로젝트에서 Microsoft SQL Server 2012 개체 사용
이 예제에서는 Microsoft SQL Server 2012를 대상으로 하는 데이터베이스 프로젝트에 시퀀스 개체를 추가합니다.  
  
Microsoft SQL Server 2012에는 시퀀스가 도입되었습니다. 시퀀스는 시퀀스를 만들 때 지정한 사양에 따라 숫자 값의 시퀀스를 생성하는 사용자 정의 스키마 바인딩된 개체입니다. 숫자 값의 시퀀스는 지정된 간격으로 올림차순 또는 내림차순으로 생성되며 요청된 경우 순환(반복)할 수 있습니다.  시퀀스 개체에 대한 자세한 내용은 [시퀀스 번호](htttp://msdn.microsoft.com/library/ff878058(SQL.110).aspx)를 참조하세요. Microsoft SQL Server 2012의 새로운 기능에 대한 자세한 내용은 [SQL Server 2012의 새로운 기능](https://msdn.microsoft.com/library/bb500435(SQL.110).aspx)을 참조하세요.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 활용합니다.  
  
### <a name="to-add-a-new-sequence-object-to-your-project"></a>프로젝트에 새 시퀀스 개체를 추가하려면  
  
1.  **솔루션 탐색기**에서 **TradeDev** 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 선택한 후 **새 항목**을 선택합니다.  
  
2.  왼쪽 창에서 **프로그래밍 기능**을 클릭하고 **시퀀스**를 선택합니다. **추가**를 클릭하여 프로젝트에 개 개체를 추가합니다.  
  
3.  기본 코드를 다음과 같이 바꿉니다.  
  
    ```  
    CREATE SEQUENCE [dbo].[Seq1]  
    AS INT  
    START WITH 1  
    INCREMENT BY 1  
    MAXVALUE 1000  
    NO CYCLE  
    CACHE 10  
    ```  
  
4.  프로젝트의 대상 플랫폼이 Microsoft SQL Server 2012로 설정되지 않은 경우 **오류 목록**에 `CREATE SEQUENCE` 문에 대한 구문 오류가 표시됩니다. 이 문제를 해결하려면 [방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) 항목에 따라 대상 플랫폼을 변경하세요.  
  
5.  [방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md) 항목에 따라 연결된 Microsoft SQL Server 2012 서버의 데이터베이스에 프로젝트를 게시합니다.  
  
### <a name="to-use-the-new-sequence-object"></a>새 시퀀스 개체를 사용하려면  
  
1.  SQL Server 개체 탐색기에서 이전 프로시저에서 프로젝트를 게시한 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
2.  쿼리 창에 다음 코드를 붙여 넣습니다.  
  
    ```  
    DECLARE @counter INT  
    SET @counter=0  
    WHILE @counter<10  
    BEGIN  
        SET @counter = @counter +1  
         INSERT dbo.Products (Id, Name, CustomerId) VALUES (NEXT VALUE FOR dbo.Seq1, 'ProductItem'+cast(@counter as varchar), 1)  
    END   
    GO  
    ```  
  
3.  **쿼리 실행** 단추를 누릅니다.  
  
4.  **SQL Server 개체 탐색기**에서 데이터베이스의 **Products** 테이블로 이동합니다. 마우스 오른쪽 단추를 클릭하고 **데이터 보기**를 선택하여 새로 추가된 행을 검사합니다.  
  
