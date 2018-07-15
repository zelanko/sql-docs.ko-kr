---
title: 메모리 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77902cfe21cf2f486007f802c0556bd410f46d4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286379"
---
# <a name="memory-properties"></a>메모리 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 다음 표에 나열된 서버 메모리 속성을 사용할 수 있습니다. 이 속성 설정에 대한 지침을 보려면 [SQL Server 2008 R2 Analysis Services 작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539)를 참조하세요.  
  
 1과 100 사이의 값은 **실제 총 메모리** 또는 **가상 주소 공간**중 더 작은 쪽의 백분율을 나타냅니다. 100을 초과하는 값은 메모리 제한(바이트)을 나타냅니다.  
  
 **적용 대상:** 다차원 및 테이블 형식 서버 모드(다르게 표시되지 않은 경우)  
  
## <a name="properties"></a>속성  
 `LowMemoryLimit`  
 서버에서 메모리가 부족한 시점을 총 실제 메모리의 백분율로 표시한 부호 있는 64비트 배정밀도 부동 소수점 숫자 속성입니다. 이 제한에 도달하면 인스턴스는 만료된 세션을 닫고 사용되지 않는 계산을 언로드하여 천천히 캐시 메모리를 지우기 시작합니다. 서버는 이 제한 아래로 메모리를 해제하지 않습니다. 기본값은 65이며 이 경우 메모리 하한은 실제 메모리 또는 가상 주소 공간의 65% 중 더 작은 쪽으로 설정됩니다.  
  
 `TotalMemoryLimit`  
 서버가 더 적극적으로 메모리 할당을 취소하기 시작하는 임계값을 정의합니다. 기본값은 실제 메모리 또는 가상 주소 공간의 80% 중 더 작은 쪽입니다.  
  
 `TotalMemoryLimit`는 항상 `HardMemoryLimit`보다 작아야 합니다.  
  
 `HardMemoryLimit`  
 인스턴스가 메모리 사용량을 줄이기 위해 활성 사용자 세션을 적극적으로 종료하기 시작하는 메모리 임계값을 지정합니다. 종료된 모든 세션은 메모리 부족으로 인해 취소되고 있다는 오류를 수신합니다. 기본값 영 (0)를 의미 합니다 `HardMemoryLimit` 사이의 중간 값으로 설정 됩니다 `TotalMemoryLimit` 및 시스템의 실제 메모리가 프로세스 다음 가상 주소의 가상 주소 공간 보다 큰 경우 시스템의 총 실제 메모리 공간 계산을 대신 사용 됩니다 `HardMemoryLimit`합니다.  
  
 `VirtualMemoryLimit`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `VertiPaqPagingPolicy`  
 서버의 메모리가 부족한 경우에 발생하는 페이징 동작을 지정합니다. 유효한 값은 다음과 같습니다.  
  
 0(**0**)은 페이징을 사용하지 않도록 설정합니다. 메모리가 부족하면 메모리 부족 오류로 처리가 실패합니다. 페이징을 사용하지 않도록 설정한 경우 서비스 계정에 대한 권한을 Windows에 부여해야 합니다. 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](../instances/configure-service-accounts-analysis-services.md)을 참조하세요.  
  
 **1** 은 기본값이며 운영 체제 페이지 파일(pagefile.sys)을 통해 디스크로의 페이징을 사용하도록 설정합니다.  
  
 때 `VertiPaqPagingPolicy` 설정 되어 1로 처리는 서버는 지정 된 메서드를 사용 하 여 디스크로 페이징을 시도 하기 때문에 메모리 제약 조건으로 인해 실패할 가능성이 적습니다. `VertiPaqPagingPolicy`속성을 설정한다고 해서 메모리 오류가 절대로 발생하지 않는 것은 아닙니다. 다음과 같은 상황에서 메모리 부족 오류가 여전히 발생할 수 있습니다.  
  
-   모든 사전에 대해 메모리가 충분하지 않습니다. Analysis Services 메모리의 각 열에 대해 사전을 잠그며 처리 중 이며 지정 된 값 보다 더 많은 일 수 없습니다 모든 합 `VertiPaqMemoryLimit`합니다.  
  
-   프로세스를 수용하기에 가상 주소 공간이 부족합니다.  
  
 지속적인 메모리 오류를 해결하려면 처리해야 할 데이터의 양을 줄이도록 모델을 다시 디자인하거나, 컴퓨터에 메모리를 추가합니다.  
  
 테이블 형식 서버 모드에만 적용됩니다.  
  
 `VertiPaqMemoryLimit`  
 디스크로의 페이징이 허용되는 경우 이 속성은 페이징이 시작되는 메모리 소비 수준(총 메모리에 대한 백분율)을 지정합니다. 기본값은 60입니다. 메모리 소비가 60% 이하이면 서버가 디스크로 페이징하지 않습니다.  
  
 이 속성에 따라 달라 집니다는 `VertiPaqPagingPolicyProperty`, 페이징이 발생 하는 1로 설정 해야 합니다.  
  
 테이블 형식 서버 모드에만 적용됩니다.  
  
 `HighMemoryPrice`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `MemoryHeapType`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 다차원 서버 모드에만 적용됩니다.  
  
 `HeapTypeForObjects`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 다차원 서버 모드에만 적용됩니다.  
  
 `DefaultPagesCountToReuse`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `HandleIA64AlignmentFaults`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `MidMemoryPrice`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `MinimumAllocatedMemory`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `PreAllocate`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `SessionMemoryLimit`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 `WaitCountIfHighMemory`  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services의 서버 속성 구성](server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
