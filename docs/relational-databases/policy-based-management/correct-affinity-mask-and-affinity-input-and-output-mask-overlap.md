---
title: 올바른 선호도 마스크 및 선호도 IO 마스크 겹침 정책
description: SQL Server에서 정책 기반 관리의 선호도 마스크 및 선호도 I/O 마스크 옵션에 모두 사용하도록 할당된 하나 이상의 프로세서가 SQL Server 인스턴스에 있는지 여부를 확인하는 정책을 사용하도록 설정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b225710aaadf3ea605e3cffd91a5a4fea2a51e62
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557802"
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>Correct Affinity Mask and Affinity Input and Output Mask Overlap
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 규칙은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 선호도 마스크 및 선호도 I/O 마스크 옵션을 모두 사용하도록 지정된 하나 이상의 프로세서가 있는지 여부를 검사합니다. 프로세서가 두 개 이상인 컴퓨터에서 선호도 마스크 및 선호도 I/O 마스크 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되는 CPU를 지정하는 데 사용됩니다. 선호도 마스크 및 선호도 I/O 마스크를 모두 사용하도록 CPU를 지정하면 프로세서가 과도하게 사용되어 성능이 저하될 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 선호도 마스크 또는 선호도 I/O 마스크 옵션을 지정할 때는 두 옵션을 모두 지정하되 각 CPU를 한 번만 활성화해야 합니다.  
  
 선호도 마스크 옵션과 선호도 I/O 마스크 옵션 모두에 대해 동일한 CPU를 활성화하면 안 됩니다. 각 CPU에 해당하는 비트의 상태는 다음 중 하나여야 합니다.  
  
-   선호도 마스크 옵션과 선호도 I/O 마스크 옵션에서 모두 0  
  
-   선호도 마스크 옵션에서는 0, 선호도 I/O 마스크 옵션에서는 1  
  
-   선호도 마스크 옵션에서는 1, 선호도 I/O 마스크 옵션에서는 0  
  
## <a name="for-more-information"></a>참조 항목  
 [affinity mask 서버 구성 옵션](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [선호도 입력-출력 마스크 서버 구성 옵션](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [affinity64 mask 서버 구성 옵션](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [affinity64 Input-Output mask 서버 구성 옵션](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
