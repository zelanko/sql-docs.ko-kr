---
title: AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정 | Microsoft 문서
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
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d672ff1be6102477bff51dd71b9d26a98e386c8c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185382"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정
  이 규칙은 AUTO_SHRINK 데이터베이스 옵션이 OFF로 설정되었는지 검사합니다. 데이터베이스를 자주 축소 및 확장하면 물리적 조각화가 발생할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정합니다. 회수 중인 공간이 이후에 필요하지 않다면 데이터베이스를 수동으로 축소하여 해당 공간을 회수할 수 있습니다.  
  
## <a name="for-more-information"></a>참조 항목  
 Microsoft 기술 자료 문서 [315512](http://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  