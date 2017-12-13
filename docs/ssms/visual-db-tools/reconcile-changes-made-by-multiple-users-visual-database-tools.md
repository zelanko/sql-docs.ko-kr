---
title: "여러 사용자가 변경한 내용 조정(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table modifications [SQL Server], multiple users
- reconciling changes made by multiple users
- modifications made by multiple users
ms.assetid: fc7ed4f2-ad3d-47fc-a3ef-51e5bb069ef0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00eeab1dbe74e77189136b200b4f1ddfe50e218b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="reconcile-changes-made-by-multiple-users-visual-database-tools"></a>여러 사용자가 변경한 내용 조정(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 다중 사용자 환경에서는 동일한 개체를 여러 사용자가 동시에 변경할 수 있습니다. 이러한 상황은 테이블 또는 데이터베이스 다이어그램 디자이너에서 개체 구조에 대한 작업을 수행 중일 때 발생할 수도 있고, 쿼리 및 뷰 디자이너의 결과 창에 반환된 결과의 값에 대해 발생할 수도 있습니다. 이 경우 충돌이 발생할 수 있으므로 적절한 해결책이 필요합니다.  
  
## <a name="conflicts-in-the-table-or-database-diagram-designers"></a>테이블 또는 데이터베이스 다이어그램 디자이너의 충돌  
예를 들어, 테이블 디자이너에서 현재 사용자가 작업 중인 것과 동일한 테이블이나 관련 테이블을 다른 사용자가 삭제하거나 이름을 변경할 수 있습니다. 테이블을 저장하려고 하면 [데이터베이스 변경 감지 대화 상자&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md) 가 표시되어 사용자가 테이블을 연 이후 데이터베이스가 업데이트되었음을 알려 줍니다.  
  
또한 이 대화 상자에는 테이블을 저장하는 경우 영향을 받는 데이터베이스 개체의 목록이 표시됩니다. 이 때 사용자는 다음 동작 중 하나를 수행할 수 있습니다.  
  
-   테이블을 저장하고 목록의 모든 변경 내용으로 데이터베이스를 업데이트하려면 **예** 를 선택합니다.  
  
    이 동작은 동일한 데이터베이스 개체를 공유하는 다른 테이블에도 영향을 줍니다. 예를 들어 `titleauthors` 테이블의 `au_id` 열을 편집하는 동안 다른 사용자가 `au_id` 열을 통해 `titleauthors` 테이블과 연결되는 `authors` 테이블에 대한 작업을 진행하는 경우 테이블을 저장하면 다른 사용자의 테이블에 영향을 줍니다. 마찬가지로 다른 사용자가 `qty` 테이블의 `sales` 열에 CHECK 제약 조건을 정의한 경우, `qty` 열을 삭제하고 `sales` 테이블을 저장하면 다른 사용자의 CHECK 제약 조건도 영향을 받습니다.  
  
-   저장 동작을 취소하려면 **아니요** 를 선택합니다.  
  
    그런 다음 테이블을 저장하지 않고 닫습니다. 테이블을 다시 열면 데이터베이스의 최신 데이터가 적용됩니다.  
  
-   변경 내용 목록을 저장하려면 **텍스트 파일 저장** 을 선택합니다.  
  
    **데이터베이스 변경 감지** 대화 상자에 표시된 데이터베이스 변경 목록을 텍스트 파일에 저장하여 다른 사용자의 변경 원인을 조사할 수 있습니다. 예를 들어, 사용자가 삭제하려고 표시한 테이블을 다른 사용자가 편집한 경우 데이터베이스를 업데이트하기 전에 테이블을 삭제해야 할지 여부를 조사할 수 있습니다.  
  
## <a name="conflicts-in-the-query-and-view-designer"></a>쿼리 및 뷰 디자이너의 충돌  
쿼리를 실행하거나 뷰의 결과를 반환하면 [결과 창](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)에 데이터가 표시됩니다. 여러 사용자가 동일한 데이터 집합에 대해 동시에 작업을 수행하는 경우 충돌이 발생할 수 있습니다.  
  
예를 들어, 현재 사용자와 동료 사용자가 각각 `titleauthors` 테이블의 모든 데이터를 표시하도록 쿼리를 실행하는 경우를 생각해 볼 수 있습니다. 반환된 첫 번째 레코드의 첫 번째 이름을 동료 사용자가 Barb에서 Barbara로 변경한 경우, 이 시점에서 데이터베이스의 해당 필드에 있는 데이터는 Barbara이지만 현재 사용자의 쿼리 결과에는 여전히 Barb가 표시됩니다. 뒤늦게 현재 사용자가 Barbara를 입력하고 다른 행으로 포커스를 옮기면 충돌 문제를 어떻게 해결할지 묻는 메시지가 나타납니다.  
  
-   변경 내용으로 데이터베이스를 업데이트하려면 **예** 를 클릭합니다.  
  
    이렇게 하면 다른 사용자가 변경한 내용이 무시되고 현재 사용자의 변경 내용이 적용됩니다.  
  
-   결과 집합을 데이터베이스의 현재 상태로 업데이트하려면 **아니요** 를 선택합니다.  
  
    이렇게 하면 현재 사용자의 변경 내용이 무시되고 다른 사용자가 변경한 내용이 적용됩니다.  
  
-   충돌을 해결하지 않은 상태로 계속 편집하려면 **취소** 를 클릭합니다.  
  
    이 경우 변경 내용을 데이터베이스에 커밋할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 변경 감지 대화 상자&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/database-changes-detected-dialog-box-visual-database-tools.md)  
  
