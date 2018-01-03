---
title: "쿼리 편집기와 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 48725f54-a7b6-4b79-948e-965c1fe4eef1
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6fcc396dc778bdf05e2ccc701be5e032ffc4ed69
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="lesson-2-1---connecting-with-query-editor"></a>2-1단원: 쿼리 편집기와 연결
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 서버와의 연결이 끊긴 동안에도 코드를 쓰거나 편집할 수 있습니다. 이 기능은 서버를 사용할 수 없을 때나 부족한 서버 또는 네트워크 리소스를 보존하고자 할 때 유용합니다. 또한 새 쿼리 편집기 창을 열거나 코드를 다시 입력하지 않고도 쿼리 편집기의 연결을 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 변경할 수 있습니다.  
  
## <a name="coding-offline"></a>오프라인으로 코드 작성  
  
#### <a name="to-write-code-offline-and-then-connect-to-different-servers"></a>오프라인으로 코드를 작성한 다음 다른 서버에 연결하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 도구 모음에서 **데이터베이스 엔진 쿼리** 를 클릭하여 쿼리 편집기를 엽니다.  
  
2.  **데이터베이스 엔진에 연결** 대화 상자에서 **취소**를 클릭합니다. 쿼리 편집기가 열리고 쿼리 편집기의 제목 표시줄에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결되어 있지 않다는 메시지가 나타납니다.  
  
3.  코드 창에 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력합니다.  
  
    ```  
    SELECT * FROM Production.Product;  
    GO  
    ```  
  
    이 시점에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 **,**실행 **,**구문 분석 **또는**예상 실행 계획 표시 **를 클릭하여**인스턴스에 연결할 수 있습니다. 이 모든 명령은 **쿼리** 메뉴, 쿼리 편집기 도구 모음 또는 쿼리 편집기 창에서 마우스 오른쪽 단추를 클릭할 때 나타나는 바로 가기 메뉴에서 사용할 수 있습니다. 이 연습에서는 도구 모음을 사용합니다.  
  
4.  도구 모음에서 **실행** 단추를 클릭하여 **데이터베이스 엔진에 연결** 대화 상자를 엽니다.  
  
5.  **서버 이름** 입력란에 서버 이름을 입력한 다음 **옵션**을 클릭합니다.  
  
6.  **연결 속성** 탭의 **연결할 데이터베이스** 목록에서 서버를 찾아 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 를 선택한 다음 **연결**을 클릭합니다.  
  
7.  같은 연결을 사용하여 다른 쿼리 편집기 창을 열려면 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
8.  연결을 변경하려면 쿼리 편집기 창에서 마우스 오른쪽 단추를 클릭하고 **연결**을 가리킨 다음 **연결 변경**을 클릭합니다.  
  
9. **SQL Server에 연결** 대화 상자에서 사용 가능한 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택한 다음 **연결**을 클릭합니다.  
  
이 새로운 쿼리 편집기 기능을 사용하면 여러 서버에서 같은 코드를 쉽게 실행할 수 있습니다. 이 기능은 여러 비슷한 서버와 관련된 유지 관리 동작에 유용합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[들여쓰기 추가](../../tools/sql-server-management-studio/lesson-2-2-adding-indentation.md)  
  
  
  
