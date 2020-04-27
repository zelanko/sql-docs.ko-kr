---
title: 쿼리 및 뷰 디자이너에 국가별 데이터 사용 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Visual Database Tools [SQL Server], international data
- queries [SQL Server], international data
- languages [SQL Server], Query and View Designer
- international considerations [SQL Server], Query and View Designer
- Criteria pane
- View Designer, international data
- Query Designer [SQL Server], international data
- localized information in Query and View Designer [SQL Server]
- global considerations [SQL Server], Query and View Designer
- SQL pane [Visual Database Tools]
- multiple language support [SQL Server], Query and View Designer
ms.assetid: 4b51c56f-f902-4e72-b919-e36127369b63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 673ad13ff5688fb17eaa4b975644256f072a3aef
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63204623"
---
# <a name="use-the-query-and-view-designer-with-international-data-visual-database-tools"></a>쿼리 및 뷰 디자이너에 국가별 데이터 사용(Visual Database Tools)
  [쿼리 및 뷰 디자이너](visual-database-tools.md) 는 모든 언어 및 모든 Windows 운영 체제 버전에서 사용할 수 있습니다. 다음 지침은 이러한 상황에서 나타나는 차이점을 요약한 것이며, 국가별 애플리케이션에서 데이터를 관리하는 방법에 대해 설명합니다.  
  
## <a name="localized-information-in-the-criteria-and-sql-panes"></a>조건 창 및 SQL 창의 지역화 정보  
 조건 창을 사용하여 쿼리를 만드는 경우 사용자의 컴퓨터에 설정된 Windows 국가별 설정에 맞는 형식으로 정보를 입력할 수 있습니다. 예를 들어, 날짜를 검색하는 경우 아래 사항을 제외하고는 편의에 따라 어떤 형식으로든 조건 열에 날짜를 입력할 수 있습니다.  
  
-   긴 데이터 형식은 지원되지 않습니다.  
  
-   조건 창에는 통화 기호를 입력할 수 없습니다.  
  
-   결과 창에서는 통화 기호가 표시되지 않습니다.  
  
    > [!NOTE]  
    >  결과 창에서 컴퓨터의 Windows 국가별 설정에 해당하는 통화 기호를 실제로 입력할 수는 있지만 결과 창에는 기호가 제거되어 표시되지 않습니다.  
  
-   단항 마이너스는 국가별 설정 옵션과 관계 없이 항상 왼쪽(예: -1)에 나타납니다.  
  
 이와 달리 SQL 창의 데이터와 키워드는 항상 ANSI(미국) 형식으로 표시해야 합니다. 예를 들어, 쿼리를 만들 때 쿼리 및 뷰 디자이너는 SELECT 및 FROM과 같은 모든 SQL 키워드를 ANSI 형식으로 삽입합니다. SQL 창에서 문에 요소를 추가하는 경우 반드시 해당 요소에 ANSI 표준 형식을 사용해야 합니다.  
  
 지역별 형식을 사용하여 데이터를 조건 창에 입력하는 경우 쿼리 및 뷰 디자이너는 SQL 창에서 해당 데이터를 ANSI 형식으로 자동 변환합니다. 예를 들어, 국가별 설정이 표준 독일어로 설정되어 있는 경우 조건 창에 "31.12.96" 같은 형식으로 날짜를 입력할 수 있지만, SQL 창에는 날짜가 `{ ts '1996-12-31 00:00:00' }.` 와 같이 ANSI 날짜 시간 형식으로 표시됩니다. SQL 창에 데이터를 직접 입력하려면 ANSI 형식을 사용해야 합니다.  
  
## <a name="sort-order"></a>정렬 순서  
 쿼리에서 데이터의 정렬 순서는 데이터베이스에 의해 결정됩니다. Windows 국가별 설정 대화 상자에서 설정한 옵션은 쿼리의 정렬 순서에 영향을 주지 않습니다. 그러나 특정 쿼리에서는 행을 특정 순서로 반환하도록 요청할 수 있습니다.  
  
## <a name="using-double-byte-characters"></a>더블바이트 문자 사용  
 테이블, 뷰 이름, 별칭 등의 리터럴 및 데이터베이스 개체 이름에 DBCS 문자를 입력할 수 있습니다. 또한 매개 변수 이름과 매개 변수 표식 문자에 DBCS 문자를 사용할 수도 있습니다. 그러나 DBCS 문자를 함수 이름 또는 SQL 키워드 같은 SQL 언어 요소에 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
