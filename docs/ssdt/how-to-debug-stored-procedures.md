---
title: '방법: 저장 프로시저 디버깅 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.EXECUTESTOREDPROCEDURE.DIALOG
ms.assetid: e3c8707f-0f6b-4265-8a5a-81f079330b52
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 727117a31fd1a2fc5f5a807de824a8ff61ebb5bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090204"
---
# <a name="how-to-debug-stored-procedures"></a>방법: 저장된 프로시저 디버깅
Transact\-SQL 디버거를 사용하면 SQL 저장 프로시저의 SQL 호출 스택, 지역 변수 및 매개 변수를 표시하여 저장 프로시저를 대화식으로 디버그할 수 있습니다. 다른 프로그래밍 언어로 디버그할 때와 마찬가지로 Transact\-SQL 스크립트를 디버그하는 동안 지역 변수 및 매개 변수를 보고 수정하고, 전역 변수를 볼 수 있을 뿐 아니라, 중단점을 제어 및 관리할 수도 있습니다.  
  
이 예에서는 Transact\-SQL 저장 프로시저를 만들고 이를 한 단계씩 실행하여 디버그하는 방법을 보여줍니다.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 절차에서 만들어진 엔터티를 사용합니다.  
  
### <a name="to-debug-stored-procedures"></a>저장 프로시저를 디버깅하려면  
  
1.  **솔루션 탐색기**에서 **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 선택한 후 **저장 프로시저**를 선택합니다. 이 새 저장 프로시저의 이름을 **AddProduct**로 지정하고 **추가**를 클릭합니다.  
  
2.  저장 프로시저에 다음 코드를 붙여 넣습니다.  
  
    ```  
    CREATE PROCEDURE [dbo].[AddProduct]  
    @id int,  
    @name nvarchar(128)  
    AS  
    INSERT INTO [dbo].[Product] (Id, Name) VALUES (@id, @name)  
    ```  
  
3.  F5 키를 눌러 프로젝트를 빌드하고 배포합니다.  
  
4.  SQL Server 개체 탐색기의 **로컬** 노드에서 **TradeDev** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다.  
  
5.  쿼리 창에 다음 코드를 붙여 넣습니다.  
  
    ```  
    EXEC [dbo].[AddProduct] 50, N'Contoso';  
    GO  
    ```  
  
6.  왼쪽 창 여백을 클릭하여 `EXEC` 문에 중단점을 추가합니다.  
  
7.  Transact\-SQL 편집기 도구 모음의 녹색 화살표 단추에 있는 드롭다운 화살표를 누르고 **디버거를 사용하여 실행**을 선택하여 디버깅이 설정된 상태로 쿼리를 실행합니다.  
  
8.  또는 SQL Server 개체 탐색기에서 디버깅을 시작할 수 있습니다. **로컬** -> **TradeDev** 데이터베이스 -> **프로그래밍 기능** -> **저장 프로시저** 아래에 있는 **AddProduct** 저장 프로시저를 마우스 오른쪽 단추로 클릭합니다. **프로시저 디버그...** 를 선택합니다. 개체에 매개 변수가 필요한 경우 각 매개 변수의 행이 포함된 테이블이 있는 **프로시저 디버그** 대화 상자가 나타납니다. 테이블의 각 행에는 매개 변수의 이름 열과 해당 매개 변수의 값 열이 있습니다. 각 매개 변수의 값을 입력하고 확인을 클릭합니다.  
  
9. **지역** 창이 열려 있는지 확인합니다. 창이 열려 있지 않으면 **디버그** 메뉴를 클릭하고 **창**을 선택한 후 **로컬**을 선택합니다.  
  
10. F11 키를 눌러 쿼리를 한 단계씩 실행합니다. 저장 프로시저의 매개 변수와 해당 값이 **지역** 창에 표시됩니다. 또는 마우스를 `INSERT` 절의 `@name` 매개 변수 위에 놓아도 할당될 **Contoso** 값이 표시됩니다.  
  
11. 텍스트 상자에서 **Contoso**를 클릭합니다. 디버그하는 동안 **Fabrikam**을 입력하고 Enter 키를 눌러 `name` 변수 값을 변경합니다. **지역** 창의 값을 변경할 수도 있습니다. 이제 매개 변수의 값이 변경되었음을 나타내는 빨간색으로 표시됩니다.  
  
12. F10 키를 눌러 나머지 코드를 한 단계씩 실행합니다.  
  
13. **Product** 테이블의 데이터 뷰에 있는 새로운 내용을 보려면 SQL Server 개체 탐색기에서 **TradeDev** 데이터베이스 노드를 새로 고칩니다.  
  
14. SQL Server 개체 탐색기의 **로컬** 노드에서 **TradeDev** 데이터베이스의 **Product** 테이블을 찾습니다.  
  
15. **Product** 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다. 새 행이 테이블에 추가되었는지 확인합니다.  
  
