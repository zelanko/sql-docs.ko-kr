---
title: AUTO_CLOSE 데이터베이스 옵션을 OFF로 설정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a4353653f4a39a3e7b6dca0a22e8de358ce65c08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691500"
---
# <a name="set-the-autoclose-database-option-to-off"></a>AUTO_CLOSE 데이터베이스 옵션을 OFF로 설정
  이 규칙은 AUTO_CLOSE 옵션이 OFF로 설정되었는지 검사합니다. AUTO_CLOSE가 ON으로 설정된 경우 각 연결 이후에 데이터베이스를 열고 닫는 데 따르는 오버헤드가 증가하여 자주 액세스되는 데이터베이스에서 성능 저하가 발생할 수 있습니다. AUTO_CLOSE는 또한 각 연결 이후에 프로시저 캐시를 플러시합니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 데이터베이스가 자주 액세스되는 경우 데이터베이스의 AUTO_CLOSE 옵션을 OFF로 설정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
