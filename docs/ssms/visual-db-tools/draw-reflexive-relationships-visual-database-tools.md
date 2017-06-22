---
title: "반사 관계 그리기(Visual Database Tools) | Microsoft 문서"
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
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b3f92a8f199bf03ff3a9c0cff4aedfb8a138ebec
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>반사 관계 그리기(Visual Database Tools)
반사 관계를 만들면 테이블에 있는 하나 이상의 열을 동일한 테이블에 있는 하나 이상의 다른 열에 연결할 수 있습니다. 예를 들어, `employee` 테이블에 `emp_id` 열과 `mgr_id` 열이 있다고 가정합니다. 각 관리자는 회사의 직원이기도 하므로 테이블 내에서 관계 선을 그려 이러한 두 열을 연결합니다. 이와 같이 관계를 설정하면 테이블에 추가되는 각 관리자 ID가 기존의 직원 ID와 일치하도록 만들 수 있습니다.  
  
관계를 만들려면 먼저 테이블에 대한 기본 키나 UNIQUE 제약 조건을 정의해야 합니다. 그런 다음 기본 키 열을 일치하는 열에 연결합니다. 관계를 만들면 일치하는 열이 테이블의 외래 키가 됩니다.  
  
### <a name="to-draw-a-reflexive-relationship"></a>반사 관계를 그리려면  
  
1.  데이터베이스 다이어그램에서 다른 열에 연결하려는 데이터베이스 열에 대한 행 선택기를 클릭하고 포인터를 테이블 바깥으로 끌어 선을 표시합니다.  
  
2.  선을 다시 선택된 테이블로 끌어 옵니다.  
  
3.  마우스 단추를 놓습니다. **테이블 및 열** 대화 상자가 나타납니다.  
  
4.  관계를 형성하려는 외래 키 열과 기본 키 테이블 및 열을 선택합니다.  
  
5.  **확인** 을 두 번 선택하여 관계를 만듭니다.  
  
테이블에 대해 쿼리를 실행할 때 반사 관계를 사용하여 자체 조인을 만들 수 있습니다. 조인을 사용하여 테이블을 쿼리하는 방법에 대한 자세한 내용은 [조인을 사용한 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[조인을 사용한 쿼리&amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  

