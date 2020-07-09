---
title: 신뢰할 수 있는 비트 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7c0fe0b7b8890b3ef9ee2671b4926c8be99cc679
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727291"
---
# <a name="trustworthy-bit"></a>신뢰할 수 있는 비트
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 규칙은 데이터베이스의 dbo 역할이 sysadmin 고정 서버 역할에 할당되어 있고 데이터베이스의 신뢰할 수 있는 비트가 ON으로 설정되었는지를 확인합니다.  
  
 이러한 조건이 충족될 경우 권한이 있는 데이터베이스 사용자가 권한을 sysadmin 역할로 승격할 수 있습니다. 이 역할에서 사용자는 시스템을 손상시킬 수 있는 안전하지 않은 어셈블리를 만들고 실행할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 신뢰할 수 있는 비트를 OFF로 설정하거나 dbo 데이터베이스 역할에서 sysadmin 권한을 취소합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
