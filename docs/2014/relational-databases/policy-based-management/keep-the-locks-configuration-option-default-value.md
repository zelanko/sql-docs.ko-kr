---
title: 잠금 구성 옵션의 기본값 유지 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d2ef15536a79b5e67de7907ce6a8bdf5595c49f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280866"
---
# <a name="keep-the-locks-configuration-option-default-value"></a>잠금 구성 옵션의 기본값 유지
  이 규칙은 잠금 구성 옵션의 값을 검사합니다. 이 옵션은 사용 가능한 잠금의 최대 개수를 결정합니다. 이 옵션은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 잠금에 사용하는 메모리 양을 제한합니다. 기본 설정은 0을 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 시스템 요구 사항의 변화를 기준으로 동적으로 잠금 구조를 할당하거나 할당 취소할 수 있습니다.  
  
 잠금이 0이 아니면, 일괄 처리 작업이 중지되고, 지정된 값이 초과될 경우 "잠금 부족" 오류 메시지가 생성됩니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 sp_configure 시스템 저장 프로시저를 다음과 같이 사용하여 잠금 값을 기본 설정으로 변경합니다.  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## <a name="for-more-information"></a>참조 항목  
 [locks 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
 [sys.dm_os_wait_stats&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)  
  
 [Microsoft 기술 자료 문서 271509](http://go.microsoft.com/fwlink/?linkid=117788)  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
