---
title: "들여쓰기 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 9dce05c1-c52f-455d-8b8d-6f303e242760
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c5e404ace201b429d97ae6427b16e0dcb2b47c21
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-2-2---adding-indentation"></a>2-2단원 - 들여쓰기 추가
쿼리 편집기를 사용하여 한 단계로 여러 코드 섹션을 들여쓸 수 있으며 들여쓰기 크기도 변경할 수 있습니다.  
  
## <a name="indenting-code"></a>코드 들여쓰기  
  
#### <a name="to-indent-multiple-lines-of-code"></a>여러 줄의 코드를 들여쓰려면  
  
1.  도구 모음에서 **새 쿼리**를 클릭합니다.  
  
2.  **Person**스키마의 **Person**테이블에서 **BusinessEntityID** , FirstName, **MiddleName** 및 **LastName** 열을 선택하는 두 번째 쿼리를 만듭니다. 코드가 다음과 같이 되도록 각 열을 별도의 줄에 배치합니다.  
  
    ```  
    -- Search for a contact  
    SELECT   
    BusinessEntityID,  
    FirstName,   
    MiddleName,   
    LastName  
    FROM Person.Person  
    WHERE LastName = 'Sanchez';  
    GO  
    ```  
  
3.  `BusinessEntityID` 에서 `LastName`에 이르는 모든 텍스트를 선택합니다.  
  
4.  **SQL 편집기** 도구 모음에서 **들여쓰기** 를 클릭하여 한 번에 모든 줄을 들여씁니다.  
  
#### <a name="to-change-the-default-indentation"></a>기본 들여쓰기를 변경하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **텍스트 편집기**, **모든 언어**를 차례로 확장하고 **탭** 을 클릭한 다음 들여쓰기 값을 적절히 설정합니다. 들여쓰기 크기뿐 아니라 탭 크기와 탭이 공백으로 변환되는지 여부도 변경할 수 있습니다.  
  
    ![탭 대화 상자의 모양](./media/lesson-2-2-adding-indentation/tabsdialog.gif "탭 대화 상자의 모양")  
  
3.  **확인**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[쿼리 편집기 화면 크기](../../tools/sql-server-management-studio/lesson-2-3-maximizing-query-editor.md)  
  
  
  
