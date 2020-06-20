---
title: 쿼리 및 뷰 디자이너의 조인 표시 방법 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
author: stevestein
ms.author: sstein
ms.openlocfilehash: f91e8f226fe97cdced78deb6b8c239806461d426
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067185"
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>쿼리 및 뷰 디자이너의 조인 표시 방법(Visual Database Tools)
  테이블이 조인되면 [쿼리 및 뷰 디자이너](visual-database-tools.md) 는 [다이어그램 창](diagram-pane-visual-database-tools.md) 에 조인을 그래픽으로 나타내고 [SQL 창](sql-pane-visual-database-tools.md)에 SQL 구문을 사용합니다.  
  
## <a name="diagram-pane"></a>다이어그램 창  
 다이어그램 창에서 쿼리 및 뷰 디자이너는 조인에 포함된 데이터 열 사이에 조인 선을 표시합니다. 쿼리 및 뷰 디자이너는 각 조인 조건에 대해 한 개의 조인 선을 표시합니다. 예를 들어, 아래 그림은 조인된 두 테이블 사이에 있는 조인 선을 보여 줍니다.  
  
 ![조인 선은 두 테이블 간 관계를 보여 줌](../../database-engine/media//dv3wbig.gif "조인 선은 두 테이블 간 관계를 보여 줌")  
  
 테이블이 두 개 이상의 조인 조건을 사용하여 조인된 경우 쿼리 및 뷰 디자이너는 다음 예에서와 같이 여러 개의 조인 선을 표시합니다.  
  
 ![둘 이상의 조인 조건을 사용하여 테이블 조인](../../database-engine/media//dv3w9n1.gif "둘 이상의 조인 조건을 사용하여 테이블 조인")  
  
 예를 들어, 테이블 또는 테이블 구조 개체를 나타내는 사각형이 최소화되거나 조인에 식이 포함되어 조인된 데이터 열이 표시되지 않는 경우 쿼리 및 뷰 디자이너는 테이블 또는 테이블 구조 개체를 나타내는 사각형의 제목 표시줄에 조인 선을 표시합니다.  
  
 조인 선의 가운데 있는 아이콘 모양은 테이블 또는 테이블 구조 개체가 조인되는 방법을 보여 줍니다. 조인 절이 등호(=) 이외의 연산자를 사용하는 경우 조인 선 아이콘에 해당 연산자가 표시됩니다. 다음 표는 조인 선에 표시되는 아이콘 목록입니다.  
  
|**조인 선 아이콘**|**설명**|  
|------------------------|---------------------|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbih.gif "Visual Database Tools 아이콘")|등호(=)를 사용하여 만든 내부 조인|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbii.gif "Visual Database Tools 아이콘")|">" 연산자를 기반으로 하는 내부 조인|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbij.gif "Visual Database Tools 아이콘")|관련 테이블에 일치하는 내용이 없는 경우에도 왼쪽에 나타난 테이블의 모든 행을 포함하는 외부 조인|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbik.gif "Visual Database Tools 아이콘")|관련 테이블에 일치하는 내용이 없는 경우에도 오른쪽에 나타난 테이블의 모든 행을 포함하는 외부 조인|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbil.gif "Visual Database Tools 아이콘")|관련 테이블에 일치하는 내용이 없는 경우에도 양쪽 테이블의 모든 행을 포함하는 완전 외부 조인|  
  
 조인 선의 끝에 있는 기호는 조인 형식을 나타냅니다. 다음 표는 조인 형식과 조인 선의 끝에 표시되는 아이콘 목록입니다.  
  
|**조인 선 끝의 아이콘**|**조인 형식**|  
|-----------------------------------|----------------------|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbim.gif "Visual Database Tools 아이콘")|일 대 일 조인|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbin.gif "Visual Database Tools 아이콘")|일 대 다 조인|  
|![Visual Database Tools 아이콘](../../database-engine/media//dv3wbio.gif "Visual Database Tools 아이콘")|쿼리 및 뷰 디자이너는 조인 형식을 결정할 수 없습니다. 조인을 수동으로 만든 경우 이러한 상황이 자주 발생합니다.|  
  
## <a name="sql-pane"></a>SQL 창  
 SQL 문에서는 다양한 방법으로 조인을 표현할 수 있습니다. 정확한 구문은 사용 중인 데이터베이스 및 조인을 정의하는 방법에 따라 다릅니다.  
  
 테이블 조인과 관련된 구문 옵션은 다음과 같습니다.  
  
-   **FROM 절의 JOIN 한정자**.   키워드 INNER 및 OUTER가 조인 형식을 지정합니다. 이 구문은 ANSI 92 SQL 표준입니다.  
  
     예를 들어, 각 테이블의 `publishers` 열을 기반으로 하여 `pub_info` 테이블과 `pub_id` 테이블을 조인하는 경우 결과 SQL 문은 다음과 같습니다.  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
     외부 조인을 만드는 경우 INNER 대신에 LEFT OUTER 또는 RIGHT OUTER가 나타납니다.  
  
-   **두 테이블의 열을 비교하는 WHERE 절**.   데이터베이스에서 JOIN 구문이 지원되지 않거나 사용자가 JOIN 구문을 직접 입력한 경우 WHERE 절이 나타납니다. WHERE 절에서 조인을 만들면 두 테이블 이름이 FROM 절에 나타납니다.  
  
     예를 들어, 아래 문은 `publishers` 테이블과 `pub_info` 테이블을 조인합니다.  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Database Tools를 &#40;조인을 사용 하 여 쿼리&#41;](query-with-joins-visual-database-tools.md)   
 [조인 대화 상자&#40;Visual Database Tools&#41;](join-dialog-box-visual-database-tools.md)  
  
  
