---
title: "Visual Database Tools 디자이너 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [SQL Server]
- View Designer
- Visual Database Tools [SQL Server]
- Database Diagram Designer
- Query Designer [SQL Server]
- design tools [Visual Database Tools]
- Table Designer
- Visual Database Tools [SQL Server], designers
- Properties window [Visual Database Tools]
ms.assetid: bd0ca68e-6f69-42dd-bcb5-ce511673769c
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f54b0ec82fd9a4c5807c3633f0e78c5782599732
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="visual-database-tool-designers"></a>Visual Database Tools 디자이너
Visual Database Tools는 데이터 원본 작업을 수행하는 데 사용할 수 있는 여러 가지 디자인 도구 모음입니다. 이러한 도구를 사용하여 쿼리를 만들고, 데이터베이스 구조를 디자인하거나 수정하고, 데이터를 업데이트할 수 있습니다. 여기에 포함된 도구는 데이터베이스 다이어그램 디자이너, 테이블 디자이너, 쿼리 및 뷰 디자이너입니다.  
  
## <a name="properties-window"></a>속성 창  
속성 창은 Visual Database Tools에만 있는 특별한 기능은 아니지만 이 창을 통해 여러 가지 항목을 수정할 수 있습니다. 여기에는 테이블 등과 같이 현재 선택된 항목의 속성이 표시되고, 이 창을 사용하여 이러한 속성을 편집할 수 있습니다. 편집할 수 있는 내용은 속성 이름에서 열의 데이터 정렬에 이르기까지 다양합니다. 속성 창에는 표시되지만 다른 도구를 사용해야만 편집할 수 있는 속성도 몇 가지 있습니다.  
  
## <a name="database-diagram-designer"></a>데이터베이스 다이어그램 디자이너  
데이터베이스 다이어그램 디자이너에는 데이터베이스의 테이블 및 관계를 시각적인 방식으로 만들고, 편집하고, 표시하는 데 사용할 수 있는 창이 있습니다.  
  
데이터베이스 다이어그램 디자이너를 표시하려면 기존 다이어그램을 열거나 개체 탐색기에서 데이터베이스 노드를 마우스 오른쪽 단추로 클릭한 다음 드롭다운 메뉴에서 **새 데이터베이스 다이어그램** 을 선택합니다.  
  
이 디자이너를 열면 주 메뉴에 **데이터베이스 다이어그램** 메뉴가 나타납니다. 이 메뉴를 통해 디자이너의 특정 기능을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 디자이너에는 Microsoft SQL Server 데이터베이스가 함께 사용됩니다.  
>   
> 이 버전의 Visual Database Tools는 Microsoft SQL Server 버전 7 및 이전 버전을 지원하지 않습니다.  
  
## <a name="table-designer"></a>테이블 디자이너  
테이블 디자이너는 연결된 Microsoft SQL Server 데이터베이스의 단일 테이블을 디자인하고 시각화할 수 있게 하는 비주얼 도구입니다.  
  
테이블 디자이너에는 두 개의 창이 있습니다. 위쪽 영역에는 표 형태가 표시되고, 표 형태의 각 행에는 데이터베이스 열에 대한 설명이 표시됩니다. 각 데이터베이스 열의 표 형태에는 기본 특성인 열 이름, 데이터 형식 및 null 허용 설정이 표시됩니다.  
  
테이블 디자이너의 아래쪽 영역인 열 속성 탭에는 위쪽 영역에서 선택한 열에 대한 추가 특성이 표시됩니다.  
  
테이블 디자이너에서 표 형식 섹션을 마우스 오른쪽 단추로 클릭하여 대화 상자를 열고 이 대화 상자를 통해 테이블의 관계, 제약 조건, 인덱스, 키 등을 만들거나 수정할 수도 있습니다.  
  
테이블 디자이너를 표시하려면 기존 테이블을 열거나 개체 탐색기에서 **테이블** 노드를 마우스 오른쪽 단추로 클릭한 다음 드롭다운 메뉴에서 **새 테이블 추가** 를 선택합니다.  
  
이 디자이너를 열면 주 메뉴에 테이블 디자이너 메뉴가 나타납니다. 이 메뉴를 통해 디자이너의 특정 기능을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 디자이너에는 Microsoft SQL Server 데이터베이스가 함께 사용됩니다.  
>   
> 이 버전의 Visual Database Tools는 Microsoft SQL Server 버전 7 및 이전 버전을 지원하지 않습니다.  
  
## <a name="query-and-view-designer"></a>쿼리 및 뷰 디자이너  
쿼리 및 뷰 디자이너는 매우 비슷한 방식으로 작동하는 두 개의 도구로 구성되어 있습니다. 이 두 도구 사이의 주요 차이점은 다음과 같습니다.  
  
-   뷰는 데이터베이스와 함께 저장되는 반면, 쿼리는 Visual Studio 데이터베이스 프로젝트와 함께 저장됩니다.  
  
-   쿼리 디자이너는 거의 모든 데이터 원본과 함께 사용할 수 있는 반면, 뷰 디자이너는 SQL Server에만 사용할 수 있습니다.  
  
-   쿼리 디자이너를 사용하면 SELECT, INSERT, UPDATE 및 DELETE DML 문을 디자인할 수 있는 반면, 뷰에는 SELECT 문만 포함될 수 있습니다.  
  
### <a name="view-designer"></a>뷰 디자이너  
뷰 디자이너를 사용하면 현재 연결되어 있는 Microsoft SQL Server 데이터베이스에서 기존의 뷰를 디자인하고 시각화하거나 새 뷰를 만들 수 있습니다.  
  
뷰 디자이너에는 다이어그램 창, 조건 창, SQL 창, 결과 창이라는 네 가지 창이 있습니다. 이러한 개별 창에 대한 자세한 내용은 [쿼리 및 뷰 디자이너 도구&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)를 참조하세요.  
  
뷰 디자이너를 표시하려면 기존 뷰를 열거나 개체 탐색기에서 **뷰** 노드를 마우스 오른쪽 단추로 클릭한 다음 드롭다운 메뉴에서 **새 뷰 추가**를 선택합니다.  
  
이 디자이너를 열면 주 메뉴에 **쿼리 디자이너** 메뉴가 나타납니다. 이 메뉴를 통해 디자이너의 특정 기능을 사용할 수 있습니다.  
  
> [!NOTE]  
> 이 디자이너에는 Microsoft SQL Server 데이터베이스가 함께 사용됩니다.  
>   
> 이 버전의 Visual Database Tools는 Microsoft SQL Server 버전 7 및 이전 버전을 지원하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
[데이터베이스 다이어그램 디자인&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-database-diagrams-visual-database-tools.md)  
[테이블 디자인&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

