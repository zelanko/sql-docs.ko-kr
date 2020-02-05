---
title: 최대 작업자 스레드 수 설정 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 79a2ff6f86c5d1fb7e109c0d8b6ba4b35d504c10
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68009337"
---
# <a name="verify-max-worker-threads-setting"></a>최대 작업자 스레드 수 설정 검사
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 최대 작업자 스레드 수 서버 옵션에서 발생할 수 있는 잘못된 설정을 검사합니다. 최대 작업자 스레드 수 옵션을 작은 값으로 설정하면 들어오는 클라이언트 요청을 적절한 시간 내에 처리하기 위한 스레드의 수가 부족하게 되어 “스레드 고갈” 상태가 발생할 수 있습니다. 옵션을 큰 값으로 설정하면 주소 공간이 낭비될 수 있습니다. 각 활성 스레드의 소비 공간이 64비트 서버의 경우 최대 4MB에 이르기 때문입니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 최대 작업자 스레드 수 옵션을 0으로 설정합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 사용자 요청에 따라 활성 작업자 스레드의 적정 수를 자동으로 결정합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
