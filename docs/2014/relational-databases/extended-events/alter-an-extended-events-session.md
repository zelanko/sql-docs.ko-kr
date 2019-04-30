---
title: 확장 이벤트 세션 변경 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99984df84d2eb24ebf3d58f3fa697d11c5ad4a1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128603"
---
# <a name="alter-an-extended-events-session"></a>확장 이벤트 세션 변경
  확장 이벤트 세션을 만든 후 **SQL Server 확장 이벤트 마법사**를 사용하여 필요한 대로 변경할 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 활성 및 비활성 세션의 대상과 활성 세션에 대한 고급 속성 구성은 변경할 수 없습니다.  
  
 활성 및 비활성 이벤트 세션 모두에 대해 다음과 같은 변경 작업을 수행할 수 있습니다.  
  
-   세션에서 이벤트를 추가 또는 제거하고 이벤트 필드, 필터 및 동작 등의 이벤트 구성을 변경할 수 있습니다.  
  
-   이벤트 세션에서 대상을 추가 또는 제거할 수 있습니다.  
  
-   **서버 시작 시 이벤트 세션 시작** 옵션을 사용하도록 설정할 수 있습니다.  
  
 비활성 이벤트 세션에 대해 다음과 같은 추가 변경 작업을 수행할 수 있습니다.  
  
-   **이벤트 간 관계 추적** 옵션을 사용하도록 설정할 수 있습니다.  
  
-   고급 속성 구성을 변경할 수 있습니다.  
  
> [!NOTE]  
>  **SQL Server 확장 이벤트 마법사** 에서는 이벤트 세션 수정을 지원하지 않습니다.  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>SQL Server 확장 이벤트 마법사를 사용하여 확장 이벤트 세션을 변경하는 방법  
  
-   개체 탐색기에서 **관리**, **확장 이벤트**, **세션**을 차례로 확장합니다.  
  
-   변경할 세션을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
-   **속성** 대화 상자에서 적절한 변경 작업을 수행한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [쿼리 편집기를 사용하여 확장 이벤트 세션 만들기](../../database-engine/create-an-extended-events-session-using-query-editor.md)  
  
  
