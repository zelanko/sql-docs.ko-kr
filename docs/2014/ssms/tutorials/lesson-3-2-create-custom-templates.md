---
title: 사용자 지정 템플릿 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tql
- templates [Transact-SQL], creating
- templates [Transact-SQL]
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 495b03b98e6c497bfd7a1527d9e2e2d81f25b762
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62805564"
---
# <a name="create-custom-templates"></a>사용자 지정 템플릿 만들기
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 함께 많은 일반 태스크에 사용할 템플릿이 제공되지만 템플릿의 진정한 힘은 자주 만들어야 할 복잡한 스크립트의 사용자 지정 템플릿을 만드는 기능에 있습니다. 이 연습에서 소수의 매개 변수가 있는 단순 스크립트를 만들지만 템플릿은 반복되는 긴 스크립트에도 유용합니다.  
  
## <a name="using-custom-templates"></a>사용자 지정 템플릿 사용  
  
#### <a name="to-create-a-custom-template"></a>사용자 지정 템플릿을 만들려면  
  
1.  템플릿 탐색기에서 **SQL Server 템플릿**을 확장하고 **Stored Procedure**를 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 가리키고 **폴더**를 클릭합니다.  
  
2.  새 템플릿 폴더 이름으로 **Custom** 을 입력한 다음 Enter 키를 누릅니다.  
  
3.  **Custom**을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **템플릿**을 클릭합니다.  
  
4.  새 템플릿 이름으로 **WorkOrdersProc** 를 입력한 다음 **Enter**키를 누릅니다.  
  
5.  **WorkOrdersProc**를 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
6.  **데이터베이스 엔진에 연결** 대화 상자에서 연결 정보를 확인한 다음 **연결**을 클릭합니다.  
  
7.  쿼리 편집기에 다음 스크립트를 입력하여 특정 부품(이 경우 Blade)에 대한 순서를 조회하는 저장 프로시저를 만듭니다. 자습서 창에서 코드를 복사하여 붙여 넣을 수 있습니다.  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  F5 키를 눌러 이 스크립트를 실행하면 **WorkOrdersForBlade** 프로시저가 생성됩니다.  
  
9. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 클릭합니다. 새 쿼리 편집기 창이 열립니다.  
  
10. 쿼리 편집기에 **EXECUTE dbo.WorkOrdersForBlade**를 입력한 다음 F5 키를 눌러 쿼리를 실행합니다. **결과** 창에서 Blade에 대한 작업 주문 목록이 반환되는지 확인합니다.  
  
11. 템플릿 스크립트 (7 단계의 스크립트)를 편집 하 고 네 곳에서 제품 이름 블레이드를, `nvarchar(50)` <strong>이름*>*</strong> <strong> *<* product_name</strong>매개 변수로 바꿉니다.  
  
    > [!NOTE]  
    >  매개 변수에는 바꾸려는 매개 변수의 이름, 매개 변수의 데이터 형식 및 매개 변수 기본값의 세 가지 요소가 필요합니다.  
  
12. 이제 스크립트는 다음과 같습니다.  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. **파일** 메뉴에서 **WorkOrdersProc.sql 저장** 을 클릭하여 템플릿을 저장합니다.  
  
#### <a name="to-test-the-custom-template"></a>사용자 지정 템플릿을 테스트하려면  
  
1.  템플릿 탐색기에서 **Stored Procedure**, **Custom**을 차례로 확장한 다음 **WorkOrderProc**를 두 번 클릭합니다.  
  
2.  **데이터베이스 엔진에 연결** 대화 상자에서 연결 정보를 지정한 다음 **연결**을 클릭합니다. **WorkOrderProc** 템플릿의 내용이 포함된 새 쿼리 편집기 창이 열립니다.  
  
3.  **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 클릭합니다.  
  
4.  **템플릿 매개 변수 바꾸기** 대화 `product_name` 상자에서 값에 대해 **freewheel** (기본 내용 덮어쓰기)을 입력 한 다음 **확인** 을 클릭 하 여 **템플릿 매개 변수 바꾸기** 대화 상자를 닫고 쿼리 편집기에서 스크립트를 수정 합니다.  
  
5.  F5 키를 눌러 쿼리를 실행하면 프로시저가 생성됩니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [스크립트를 프로젝트 또는 솔루션으로 저장](lesson-3-3-save-scripts-as-projects-or-solutions.md)  
  
  
