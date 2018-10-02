---
title: 필터 설정(개체 탐색기 및 유틸리티 탐색기) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd99ddf8617cafc55c5437b61868e3559275c8b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832491"
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>필터 설정(개체 탐색기 및 유틸리티 탐색기)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
이 대화 상자를 사용하여 필터를 지정할 수 있습니다. 필터를 사용하면 특정 조건에 맞는 항목만 표시하도록 개체 탐색기 및 유틸리티 탐색기를 구성할 수 있습니다. 예를 들어 필터를 사용하여 이름에 "Maintenance"라는 단어가 포함된 작업만 표시할 수 있습니다. **필터 설정** 대화 상자의 머리글에는 서버 이름이나 데이터베이스 이름이 포함될 수 있습니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
**속성**  
필터링할 속성을 표시합니다.  
  
**같음**  
필터가 속성에 값을 적용하는 방식을 선택합니다. 옵션은 다음과 같습니다.  
  
-   **같음**  
  
    필터는 속성과 해당 값이 정확히 일치하는 항목을 표시합니다.  
  
-   **포함**  
  
    필터는 속성에 해당 값이 포함된 항목을 표시합니다. 속성에 다른 텍스트가 포함될 수도 있습니다.  
  
-   **포함하지 않음**  
  
    필터는 속성에 해당 값이 포함되지 않은 항목을 표시합니다.  
  
-   **보다 작음**  
  
    이 필터는 날짜에 사용할 수 있으며 해당 날짜가 제공된 값보다 이전인 항목을 표시합니다.  
  
-   **작거나 같음**  
  
    이 필터는 날짜에 사용할 수 있으며 해당 날짜가 제공된 값과 같거나 이전인 항목을 표시합니다.  
  
-   **보다 큼**  
  
    이 필터는 날짜에 사용할 수 있으며 해당 날짜가 제공된 값보다 이후인 항목을 표시합니다.  
  
-   **크거나 같음**  
  
    이 필터는 날짜에 사용할 수 있으며 해당 날짜가 제공된 값과 같거나 이후인 항목을 표시합니다.  
  
-   **사이**  
  
    이 필터는 날짜에 사용할 수 있으며 해당 날짜가 제공된 두 값 사이에 있는 항목을 표시합니다. **사이** 를 선택하고 Tab 키를 누르면 두 번째 날짜를 입력할 다른 행이 추가됩니다.  
  
-   **사이에 있지 않음**  
  
    이 필터는 날짜에 사용할 수 있으며 해당 날짜가 제공된 두 날짜보다 이전이거나 이후인 항목을 보여 줍니다. **사이에 있지 않음** 을 선택하고 **연산자** 열에서 Tab 키를 누르면 두 번째 날짜를 입력할 다른 행이 추가됩니다.  
  
**Value**  
속성과 비교할 값을 입력합니다. 날짜의 경우 아래쪽 화살표를 클릭하면 날짜를 선택할 수 있는 달력이 표시됩니다.  
  
**필터 지우기**  
현재 필터 설정을 모두 제거합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 사용](../../ssms/use-sql-server-management-studio.md)  
[SQL Server 유틸리티 개요](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
