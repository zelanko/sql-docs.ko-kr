---
title: "AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e48430038885fcdf1bcc6e89cc2feda29bc642a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="set-the-autoshrink-database-option-to-off"></a>AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정
  이 규칙은 AUTO_SHRINK 데이터베이스 옵션이 OFF로 설정되었는지 검사합니다. 데이터베이스를 자주 축소 및 확장하면 물리적 조각화가 발생할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정합니다. 회수 중인 공간이 이후에 필요하지 않다면 데이터베이스를 수동으로 축소하여 해당 공간을 회수할 수 있습니다.  
  
## <a name="for-more-information"></a>참조 항목  
 Microsoft 기술 자료 문서 [315512](http://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
