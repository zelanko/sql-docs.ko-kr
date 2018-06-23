---
title: 조인 제거(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- removing joins
- joins [SQL Server], removing
- deleting joins
ms.assetid: ccc212a1-fd13-48d6-85e5-5ff310c34bbd
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 75ee172ba9dcdb5761e7dd1eefe5722441c9983a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091182"
---
# <a name="remove-joins-visual-database-tools"></a>조인 제거(Visual Database Tools)
  내부 조인 또는 외부 조인을 통해 테이블을 더 이상 조인하지 않으려면 테이블 간의 조인을 제거하면 됩니다. 예를 들어 [쿼리 및 뷰 디자이너](visual-database-tools.md) 가 두 테이블 간에 자동으로 만든 조인을 제거할 수 있습니다.  
  
> [!NOTE]  
>  쿼리에서 조인을 제거해도 데이터베이스에서의 기본 관계는 변경되지 않습니다.  
  
 조인된 두 테이블이 쿼리의 일부인 경우 이 테이블 간의 조인 조건을 모두 제거하면 그 결과 쿼리는 두 테이블 모두의 산물이 됩니다. 즉, CROSS JOIN이 됩니다.  
  
### <a name="to-remove-a-join"></a>조인을 제거하려면  
  
-   [다이어그램 창](diagram-pane-visual-database-tools.md)에서 제거할 조인의 조인 선을 선택한 다음 Delete 키를 누릅니다. 한 번에 조인 선을 여러 개 선택하여 삭제할 수 있습니다.  
  
 쿼리 및 뷰 디자이너는 조인 선을 제거하고 [SQL 창](sql-pane-visual-database-tools.md)에서 문을 변경합니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 자동 조인 &#40;Visual Database Tools&#41;](join-tables-automatically-visual-database-tools.md)   
 [테이블을 수동으로 조인 &#40;Visual Database Tools&#41;](join-tables-manually-visual-database-tools.md)   
 [조인을 사용한 쿼리&#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)  
  
  