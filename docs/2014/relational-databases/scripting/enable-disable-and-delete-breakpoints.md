---
title: 중단점 설정, 해제 및 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 357b5874-273f-43a9-8e30-83872bdea5dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edc19f948689fafea8cde0fb4ae2fd5f79de3242
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064055"
---
# <a name="enable-disable-and-delete-breakpoints"></a>중단점 설정, 해제 및 삭제
  열려 있는 모든 중단점을 보고 관리하려면 **중단점** 창을 사용합니다. 이 창을 사용하여 중단점 정보를 보고 중단점 삭제, 해제, 설정 등과 같은 동작을 수행할 수 있습니다.  
  
## <a name="the-breakpoints-window"></a>중단점 창  
 **중단점** 창에는 중단점이 위치한 코드 줄과 같은 정보가 나열됩니다. **중단점** 창에서 중단점을 삭제, 해제 및 설정할 수 있습니다. **중단점** 창에 대한 자세한 내용은 [중단점 Window](transact-sql-debugger-breakpoints-window.md)을 참조하십시오.  
  
 중단점을 해제하면 실행이 일시 중지되지 않지만 사용자가 나중에 중단점을 설정할 경우를 위해 정의는 그대로 유지됩니다. 중단점을 삭제하면 영구적으로 제거됩니다. 문에서 실행을 일시 중지하려면 새 중단점을 설정해야 합니다.  
  
## <a name="to-open-the-breakpoints-window"></a>중단점 창을 열려면  
 **To open the Breakpoints window**  
  
 다음 방법 중 하나를 사용하여 **중단점** 창을 열 수 있습니다.  
  
-   **디버그** 메뉴에서 **창**을 클릭한 다음 **중단점**을 클릭합니다.  
  
-   **디버그** 도구 모음에서 **중단점** 단추를 클릭합니다.  
  
-   Ctrl+Alt+B를 누릅니다.  
  
## <a name="to-disable-a-single-breakpoint"></a>단일 중단점을 해제하려면  
 **To disable a single breakpoint**  
  
 다음 방법 중 하나를 사용하여 단일 중단점을 해제할 수 있습니다.  
  
-   쿼리 편집기 창에서 중단점을 마우스 오른쪽 단추로 클릭한 다음 **중단점 해제**를 클릭합니다.  
  
-   중단점 창에서 중단점 왼쪽에 있는 확인란의 선택을 취소합니다.  
  
## <a name="to-disable-all-breakpoints"></a>모든 중단점을 해제하려면  
 **To disable all breakpoints**  
  
 다음 방법 중 하나를 사용하여 모든 중단점을 해제할 수 있습니다.  
  
-   **디버그** 메뉴에서 **모든 중단점 해제**를 클릭합니다.  
  
-   **중단점** 창의 도구 모음에서 **모든 중단점 해제** 단추를 클릭합니다.  
  
## <a name="to-enable-a-single-breakpoint"></a>단일 중단점을 사용하려면  
 **To enable a single breakpoint**  
  
 다음 방법 중 하나를 사용하여 단일 중단점을 사용하도록 설정할 수 있습니다.  
  
-   쿼리 편집기 창에서 중단점을 마우스 오른쪽 단추로 클릭한 다음 **중단점 설정**을 클릭합니다.  
  
-   중단점 창에서 중단점 왼쪽에 있는 상자를 클릭합니다.  
  
## <a name="to-enable-all-breakpoints"></a>모든 중단점을 사용하려면  
 **To enable all breakpoints**  
  
 다음 방법 중 하나를 사용하여 모든 중단점을 사용하도록 설정할 수 있습니다.  
  
-   **디버그** 메뉴에서 **모든 중단점 설정**을 클릭합니다.  
  
-   **중단점** 창의 도구 모음에서 **모든 중단점 설정** 단추를 클릭합니다.  
  
## <a name="to-delete-a-single-breakpoint"></a>단일 중단점을 삭제하려면  
 **To delete a single breakpoint**  
  
 다음 방법 중 하나를 사용하여 단일 중단점을 삭제할 수 있습니다.  
  
-   쿼리 편집기 창에서 중단점을 마우스 오른쪽 단추로 클릭한 다음 **중단점 삭제**를 클릭합니다.  
  
-   중단점 창에서 중단점을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **삭제** 를 클릭합니다.  
  
-   중단점 창에서 중단점을 선택한 다음 Delete 키를 누릅니다.  
  
## <a name="to-delete-all-breakpoints"></a>모든 중단점을 삭제하려면  
 **To delete all breakpoints**  
  
 다음 방법 중 하나를 사용하여 모든 중단점을 삭제할 수 있습니다.  
  
-   **디버그** 메뉴에서 **모든 중단점 삭제**를 클릭합니다.  
  
-   **중단점** 창의 도구 모음에서 **모든 중단점 삭제** 단추를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [중단점 설정/해제](../spatial/point.md)  
  
  
