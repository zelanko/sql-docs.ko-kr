---
title: 외부 조인 만들기(Visual Database Tools) | Microsoft 문서
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
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eaa656ab6775594477ed4d83470b1c2ebab642c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-outer-joins-visual-database-tools"></a>외부 조인 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 는 기본적으로 테이블 간에 내부 조인을 만듭니다. 다른 테이블의 행과 일치하지 않는 행은 없앱니다. 그러나 외부 조인은 FROM 절에 지정된 하나 이상의 테이블이나 뷰에서 WHERE 또는 HAVING 검색 조건을 만족하는 모든 행을 반환합니다. 조인된 테이블에 일치 값이 없는 데이터 행을 결과 집합에 포함하려면 외부 조인을 만들면 됩니다.  
  
외부 조인을 만들 때는 SQL 창의 SQL 문에 테이블이 표시되는 순서가 중요합니다. 첫 번째로 추가하는 테이블이 "왼쪽" 테이블이 되고 두 번째로 추가하는 테이블이 "오른쪽" 테이블이 됩니다. [다이어그램 창](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)에 테이블이 실제로 표시되는 순서는 중요하지 않습니다. 왼쪽 또는 오른쪽 우선 외부 조인을 지정할 경우 쿼리에 테이블이 추가된 순서와 [SQL 창](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)의 SQL 문에 테이블이 표시되는 순서를 참조합니다.  
  
### <a name="to-create-an-outer-join"></a>외부 조인을 만들려면  
  
1.  자동 또는 수동으로 조인을 만듭니다. 자세한 내용은 [테이블 자동 조인&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md) 또는 [테이블 수동 조인&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md)을 참조하세요.  
  
2.  다이어그램 창에서 조인 선을 선택한 다음 **쿼리 디자이너** 메뉴에서 **<tablename>의 모든 행 선택**을 선택하여 포함하려는 여분의 행이 들어 있는 테이블을 포함하는 명령을 선택합니다.  
  
    -   첫 번째 테이블을 선택하여 왼쪽 우선 외부 조인을 만듭니다.  
  
    -   두 번째 테이블을 선택하여 오른쪽 우선 외부 조인을 만듭니다.  
  
    -   두 테이블을 모두 선택하여 완전 외부 조인을 만듭니다.  
  
외부 조인을 지정하면 쿼리 및 뷰 디자이너가 외부 조인을 나타내는 조인 선을 수정합니다.  
  
또한 쿼리 및 뷰 디자이너는 SQL 창의 SQL 문을 다음과 같이 수정하여 조인 형식의 변경 사항을 반영합니다.  
  
```  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
```  
  
외부 조인은 일치하지 않는 행을 포함하므로 FOREIGN KEY 제약 조건을 위반하는 행을 찾는 데 사용할 수 있습니다. 이를 수행하려면 외부 조인을 만든 다음 검색 조건을 추가하여 가장 오른쪽 테이블의 기본 키 열이 null인 행을 찾습니다. 예를 들어 다음 외부 조인은 `employee` 테이블에서 `jobs` 테이블의 해당 행을 포함하지 않는 행을 찾습니다.  
  
```  
SELECT employee.emp_id, employee.job_id  
FROM employee LEFT OUTER JOIN jobs   
   ON employee.job_id = jobs.job_id  
WHERE (jobs.job_id IS NULL)  
```  
  
## <a name="see-also"></a>참고 항목  
[조인을 사용한 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[조인 대화 상자&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
