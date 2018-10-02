---
title: 확장 이벤트 세션 변경 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 189a524e6e864faf76ed43647af8a34055c27b0b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774707"
---
# <a name="alter-an-extended-events-session"></a>확장 이벤트 세션 변경
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>참고 항목  
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [쿼리 편집기를 사용하여 확장 이벤트 세션 만들기](http://msdn.microsoft.com/library/cba0e02b-b201-4863-bf1b-9164e68e5fa8)  
  
  
