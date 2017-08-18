---
title: "테이블 수동 조인(Visual Database Tools) | Microsoft 문서"
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
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57821cd36a4684de594df52b0722b7e043097b46
ms.contentlocale: ko-kr
ms.lasthandoff: 08/18/2017

---
# <a name="join-tables-manually-visual-database-tools"></a>테이블 수동 조인(Visual Database Tools)
쿼리에 둘 이상의 테이블을 추가하면 [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)는 데이터베이스에 저장된 테이블 관계 정보나 공용 데이터를 기반으로 테이블을 조인합니다. 자세한 내용은 [테이블 자동 조인&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md)을 참조하세요. 하지만 쿼리 및 뷰 디자이너가 테이블을 자동으로 조인하지 않은 경우나 테이블간에 추가로 조인 조건을 만들려는 경우에는 테이블을 수동으로 조인하면 됩니다.  
  
같은 정보를 포함하는 열뿐만 아니라 임의의 두 열을 서로 비교하여 조인을 만들 수 있습니다. 데이터베이스에 `titles` 와 `roysched`라는 두 개의 테이블이 있는 경우 `ytd_sales` 테이블에 있는 `titles` 열의 값을 `lorange` 테이블에 있는 `hirange` 및 `roysched` 열의 값과 비교할 수 있습니다. 이 조인을 만들면 연간 매출 누계가 사용료 지급액의 최고/최저 범위 사이에 있는 제목을 찾을 수 있습니다.  
  
> [!TIP]  
> 조인 조건의 열이 인덱싱된 경우 조인 작업이 가장 빠르게 수행됩니다. 일부 경우 인덱싱되지 않은 열을 조인하면 쿼리 처리 속도가 느려질 수 있습니다.  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>테이블 또는 테이블 구조 개체를 수동으로 조인하려면  
  
1.  조인할 개체를 [다이어그램 창](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) 에 추가합니다.  
  
2.  첫 번째 테이블 또는 테이블 구조 개체의 조인 열 이름을 끌어서 두 번째 테이블 또는 테이블 구조 개체의 관련 열 위에 놓습니다. 조인은 **텍스트**, **ntext**또는**이미지** 열을 기반으로 할 수 없습니다.  
  
    > [!NOTE]  
    > 조인 열의 데이터 형식은 같거나 호환 가능해야 합니다. 예를 들어, 첫 번째 테이블의 조인 열이 날짜이면 이 열을 두 번째 테이블의 날짜 열과 관련시켜야 합니다. 반면에 첫 번째 조인 열이 정수이면 관련된 조인 열의 데이터 형식도 정수이어야 하지만 크기는 달라도 됩니다. 쿼리 및 뷰 디자이너는 조인을 만드는 데 사용하는 열의 데이터 형식을 검사하지 않지만 데이터 형식이 호환되지 않으면 쿼리를 실행할 때 데이터베이스에 오류 메시지가 표시됩니다.  
  
3.  필요한 경우 조인 연산자를 변경합니다. 기본 연산자는 등호(=)입니다. 자세한 내용은 [조인 연산자 수정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/modify-join-operators-visual-database-tools.md)을 참조하세요.  
  
쿼리 및 뷰 디자이너는 [SQL 창](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)의 SQL 문에 INNER JOIN 절을 추가합니다. 조인 형식을 외부 조인으로 변경할 수 있습니다. 자세한 내용은 [외부 조인 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-outer-joins-visual-database-tools.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[조인을 사용한 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  

