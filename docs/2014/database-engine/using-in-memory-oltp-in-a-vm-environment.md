---
title: VM 환경에서 메모리 내 OLTP 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 27ec7eb3-3a24-41db-aa65-2f206514c6f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f7f04b04792167fe9c4733f3e066c362f3cae4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62843079"
---
# <a name="using-in-memory-oltp-in-a-vm-environment"></a>VM 환경에서 메모리 내 OLTP 사용
  서버 가상화 기술을 사용하면 IT 자본 및 운영 비용을 줄이고 향상된 애플리케이션 프로비전, 유지 관리, 가용성 및 백업/복구 프로세스를 통해 IT 효율성을 높일 수 있습니다. 최근의 기술적 진보에 따라 가상화를 사용하면 복잡한 데이터베이스 작업도 보다 쉽고 간단하게 통합할 수 있습니다. 이 항목에서는 가상화된 환경에서 [!INCLUDE[hek_1](../includes/hek-1-md.md)] 를 사용하기 위한 모범 사례에 대해 설명합니다.  
  
##  <a name="bkmk_memoryPreAllocation"></a>메모리 사전 할당  
 가상화된 환경의 메모리에 대해 필수적으로 고려해야 할 사항은 더 나은 성능과 향상된 지원 방식입니다. 요구 사항(최대 및 최소 부하)에 따라 가상 컴퓨터에 메모리를 신속하게 할당하면서도 메모리가 낭비되지 않도록 방지하는 두 마리 토끼를 모두 잡아야 합니다. Hyper-V 동적 메모리 기능을 사용하면 호스트에서 실행되는 가상 컴퓨터 간에 메모리를 할당하고 관리하는 작업을 신속하게 수행할 수 있습니다.  
  
 메모리 최적화 테이블이 포함된 데이터베이스를 가상화할 때는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가상화 및 관리를 위한 일부 모범 사례에 대한 수정이 필요합니다. 메모리 최적화 테이블이 없는 경우의 모범 사례 중 두 가지는 다음과 같습니다.  
  
-   MIN_SERVER_MEMORY를 사용하는 경우에는 다른 프로세스용으로 메모리가 충분히 남아 있도록 필요한 양의 메모리만 할당하여 페이징이 수행되지 않도록 하는 것이 좋습니다.  
  
-   메모리 미리 할당 값은 너무 높게 설정하지 마십시오. 그렇지 않으면 다른 프로세스에 메모리가 필요할 때 충분한 메모리를 사용하지 못하게 되어 메모리 페이징이 발생할 수 있습니다.  
  
 메모리 최적화 테이블이 포함된 데이터베이스에서 위와 같은 방식을 따를 경우 데이터베이스 복구에 사용할 수 있는 메모리가 충분하더라도 데이터베이스를 복원 및 복구하려고 하면 데이터베이스가 "복구 보류 중" 상태가 될 수 있습니다. 그 이유는 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 는 시작 시 동적 메모리 할당이 데이터베이스에 메모리를 할당하는 것보다 더 많은 데이터를 메모리로 가져오기 때문입니다.  
  
 **해결책이**  
  
 이 문제를 완화하기 위해서는 필요할 때 추가 메모리를 제공하기 위한 동적 메모리에 따라 달라지는 최소 값이 아니라 데이터베이스를 복구 또는 다시 시작하기 위한 충분한 메모리를 데이터베이스에 미리 할당하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
