---
title: 쿼리 및 뷰 디자이너 열기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c899f595c0c351982f7d4e0bfbf3ad52c17f0f0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031331"
---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>쿼리 및 뷰 디자이너 열기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
쿼리 및 뷰 디자이너는 뷰의 정의를 열거나, 쿼리 또는 뷰의 결과를 표시하거나, 쿼리를 만들거나 열 때 나타납니다. 이 디자이너는 네 개의 개별 창으로 구성되어 있습니다.  
  
-   다이어그램 창은 데이터 연결에서 선택한 테이블 또는 테이블 반환 개체를 그래픽으로 표시합니다. 또한 이들 사이의 조인 관계도 보여 줍니다.  
  
-   조건 창에서 스프레드시트 모양의 표 형태에 선택한 항목을 입력하여 표시할 데이터 열, 결과 정렬 방법, 선택할 행 등의 쿼리 옵션을 지정할 수 있습니다.  
  
-   SQL 창을 사용하여 고유한 SQL 문을 만들거나 조건 창 및 다이어그램 창을 사용하여 문을 만들 수 있습니다. 조건 창이나 다이어그램 창을 사용해도 SQL 문은 SQL 창에 작성됩니다. 쿼리를 작성할 때 SQL 창은 읽기 쉽도록 자동으로 업데이트되고 서식이 다시 지정됩니다.  
  
-   결과 창은 가장 최근에 실행한 SELECT 쿼리의 결과를 보여 줍니다. 다른 쿼리 형식의 결과는 메시지 상자에 표시됩니다.  
  
-   이러한 창은 쿼리와 뷰 작업에 모두 유용하게 사용할 수 있습니다.  
  
-   뷰나 쿼리를 열면 창의 일부 또는 전체가 함께 열립니다. 이때 열리는 창은 **옵션** 대화 상자의 설정과 현재 연결되어 있는 데이터베이스 관리 시스템에 따라 달라집니다. 기본적으로 네 개의 창이 모두 열립니다.  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>뷰의 쿼리 및 뷰 디자이너를 열려면  
  
1.  개체 탐색기에서 열려는 뷰를 마우스 오른쪽 단추로 클릭한 다음 **디자인** 또는 **뷰 열기**를 클릭합니다.  
  
    **디자인**을 선택한 경우 **옵션** 대화 상자에서 선택한 옵션에 따라 쿼리 및 뷰 디자이너 창이 열립니다. **뷰 열기**를 선택한 경우에는 기본적으로 결과 창만 열립니다.  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>기존 쿼리에 대해 쿼리 및 뷰 디자이너를 열려면  
  
1.  솔루션 탐색기에서 **쿼리** 폴더를 확장합니다.  
  
2.  열려는 쿼리를 두 번 클릭합니다.  
  
3.  해당 쿼리 문을 강조 표시하고 강조 표시된 영역을 마우스 오른쪽 단추로 클릭한 다음 **편집기에서 쿼리 디자인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 및 뷰 디자이너 도구&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  
