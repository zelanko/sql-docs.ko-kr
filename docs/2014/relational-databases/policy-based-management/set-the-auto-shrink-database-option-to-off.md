---
title: AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c81885e5a3aaec197b8963c2e868b6f65a0b0544
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62691519"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정
  이 규칙은 AUTO_SHRINK 데이터베이스 옵션이 OFF로 설정되었는지 검사합니다. 데이터베이스를 자주 축소 및 확장하면 물리적 조각화가 발생할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 AUTO_SHRINK 데이터베이스 옵션을 OFF로 설정합니다. 회수 중인 공간이 이후에 필요하지 않다면 데이터베이스를 수동으로 축소하여 해당 공간을 회수할 수 있습니다.  
  
## <a name="for-more-information"></a>참조 항목  
 Microsoft 기술 자료 문서 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
