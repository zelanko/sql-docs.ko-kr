---
title: 메모리 속성 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c3542d8ffff4c5c8887c5c0f8f8747e4714dcd5c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="memory-properties"></a>메모리 속성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 은 요청을 즉시 처리할 수 있도록 시작 시 적절한 메모리 양을 사전 할당합니다. 쿼리 및 처리 작업이 증가함에 따라 추가 메모리가 할당됩니다. 
  
  구성 설정을 지정하여 메모리가 해제되는 임계값을 제어할 수 있습니다. 예를 들어 **HardMemoryLimit** 설정은 더 많은 리소스를 사용할 수 있을 때까지 새로운 요청이 완전히 거부되는 자체 부과된 메모리 부족 조건을 지정합니다(기본적으로 이 임계값은 사용되지 않음).

최대 메모리 버전별 Analysis Services 인스턴스 당 사용량에 대 한 자세한 참조 [버전 및 SQL Server의 지원 되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)합니다.
  
 다음 설정은 별도로 언급 하지 않는 한 두 다차원 모델과 테이블 형식 서버 모드에 적용 됩니다.  
 
## <a name="default-memory-configuration"></a>기본 메모리 구성

기본 구성에서 각 Analysis Services 인스턴스는 인스턴스가 유휴 상태인 경우에도 시작 시 소량의 RAM(40-50MB)을 할당합니다. 

구성 설정은 인스턴스별로 지정됩니다. 동일한 하드웨어에서 테이블 형식 및 다차원 인스턴스 등 Analysis Services의 여러 인스턴스를 실행하는 경우 각 인스턴스가 다른 인스턴스와 독립적으로 자체 메모리를 할당합니다.

아래 표에서는 자주 사용되는 메모리 설정을 간략하게 설명합니다(참조 섹션에 자세한 내용이 포함되어 있음). 이러한 설정은 Analysis Services가 동일한 서버의 다른 응용 프로그램과 메모리를 경쟁하는 경우에 구성해야 합니다.

설정 | Description
--------|------------
LowMemoryLimit | 다차원 인스턴스에서 서버가 자주 사용되지 않는 개체에 할당된 메모리를 처음 해제하기 시작하는 하한 임계값입니다.
VertiPaqMemoryLimit | 테이블 형식 인스턴스에서 서버가 자주 사용되지 않는 개체에 할당된 메모리를 처음 해제하기 시작하는 하한 임계값입니다.
TotalMemoryLimit | Analysis Services가 실행 중인 요청과 우선 순위가 높은 새 요청을 위한 공간을 확보하기 위해 더 적극적으로 메모리 해제를 시작하는 상한 임계값입니다. 
HardMemoryLimit | Analysis Services가 메모리 압력으로 인해 완전히 요청을 거부하기 시작하는 또 다른 임계값입니다. 
 
## <a name="property-reference"></a>속성 참조

다음 속성은 달리 지정되지 않은 경우 테이블 형식 및 다차원 모드 둘 다에 적용됩니다.

 1과 100 사이의 값은 **실제 총 메모리** 또는 **가상 주소 공간**중 더 작은 쪽의 백분율을 나타냅니다. 100을 초과하는 값은 메모리 제한(바이트)을 나타냅니다.
  
 **LowMemoryLimit**  
 Analysis Services가 자주 사용되지 않는 캐시 등 우선 순위가 낮은 개체에 대한 메모리 해제를 시작하는 첫 번째 임계값을 정의하는 부호 있는 64비트 배정밀도 부동 소수점 숫자 속성입니다. 메모리가 할당되고 나면 서버에서 이 제한 아래로 메모리를 해제하지 않습니다. 기본값은 65이며 이 경우 메모리 하한은 실제 메모리 또는 가상 주소 공간의 65% 중 더 작은 쪽으로 설정됩니다.  
  
 **TotalMemoryLimit**  
 서버가 다른 요청을 위한 공간을 확보하기 위해 메모리 할당을 취소하기 시작하는 임계값을 정의합니다. 이 제한에 도달하면 인스턴스는 만료된 세션을 닫고 사용되지 않는 계산을 언로드하여 천천히 캐시 메모리를 지우기 시작합니다. 기본값은 실제 메모리 또는 가상 주소 공간의 80% 중 더 작은 쪽입니다. **TotalMemoryLimit** 는 항상 **HardMemoryLimit**보다 작아야 합니다.  
  
 **HardMemoryLimit**  
 인스턴스가 메모리 사용량을 줄이기 위해 활성 사용자 세션을 적극적으로 종료하기 시작하는 메모리 임계값을 지정합니다. 종료된 모든 세션은 메모리 부족으로 인해 취소되고 있다는 오류를 수신합니다. 기본값 영(0)은 **HardMemoryLimit** 가 **TotalMemoryLimit** 와 시스템의 실제 총 메모리 사이의 중간 값으로 설정됨을 의미합니다. 시스템의 실제 메모리가 프로세스의 가상 주소 공간보다 큰 경우 **HardMemoryLimit**를 계산할 때 가상 주소 공간이 대신 사용됩니다.  
  
 **VirtualMemoryLimit**  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **VertiPaqPagingPolicy**  
  테이블 형식 인스턴스에만 적용되며, 서버의 메모리가 부족한 경우에 발생하는 페이징 동작을 지정합니다. 유효한 값은 다음과 같습니다.  
  
  

설정  |Description  
---------|---------
**0**     |  페이징을 사용하지 않도록 설정합니다. 메모리가 부족하면 메모리 부족 오류로 처리가 실패합니다. 페이징을 사용하지 않도록 설정한 경우 서비스 계정에 대한 권한을 Windows에 부여해야 합니다. 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)을 참조하세요. 
**1**     |  (기본값) 운영 체제 페이지 파일(pagefile.sys)을 통해 디스크로의 페이징을 사용하도록 설정합니다.   
  
1로 설정될 경우 서버는 지정된 방법을 사용하여 디스크로 페이징을 시도하기 때문에 메모리 제약 조건으로 인해 처리가 실패할 가능성이 적습니다. **VertiPaqPagingPolicy** 속성을 설정한다고 해서 메모리 오류가 절대로 발생하지 않는 것은 아닙니다. 다음과 같은 상황에서 메모리 부족 오류가 여전히 발생할 수 있습니다.  
  
-   모든 사전에 대해 메모리가 충분하지 않습니다. 처리 중 Analysis Services는 메모리의 각 열에 대해 사전을 잠그며 이 모든 합은 **VertiPaqMemoryLimit**에 대해 지정된 값보다 클 수 없습니다.  
  
-   프로세스를 수용하기에 가상 주소 공간이 부족합니다.  
  
 지속적인 메모리 오류를 해결하려면 처리해야 할 데이터의 양을 줄이도록 모델을 다시 디자인하거나, 컴퓨터에 메모리를 추가합니다.  
  
 **VertiPaqMemoryLimit**  
 테이블 형식 인스턴스에만 적용되며, 디스크로의 페이징이 허용되는 경우 이 속성은 페이징이 시작되는 메모리 소비 수준(총 메모리에 대한 백분율)을 지정합니다. 기본값은 60입니다. 메모리 소비가 60% 이하이면 서버가 디스크로 페이징하지 않습니다. 이 속성을 사용하려면 **VertiPaqPagingPolicyProperty**를 1로 설정하여 페이징이 발생할 수 있도록 해야 합니다.  
  
 **HighMemoryPrice**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryHeapType**  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다. SQL Server 2016 SP1 이상 Analysis Services의 유효한 값은 다음과 같습니다.
  
  설정 | Description
--------|------------
**-1** | (기본값) 자동. 사용할 항목을 엔진이 결정합니다.
**1** | Analysis Services 힙
**2** | Windows LFH
**5** | 하이브리드 할당자. 이 할당자에 대 한 Windows LFH \<16KB 할당 및에 대 한 AS 힙 = > 16KB 할당 합니다. 
**6** | Intel TBB 할당자. SQL Server 2016 SP1 이상 Analysis Services에서 사용할 수 있습니다.
  
  
 **HeapTypeForObjects**  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다. 유효한 값은 다음과 같습니다.
  
   설정 | Description
--------|------------
**0** | Windows LFH 힙
**1** | Analysis Services 슬롯 할당자.
**3** | 각 개체에 자체 Analysis Services 힙이 있습니다.

 
 **DefaultPagesCountToReuse**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **HandleIA64AlignmentFaults**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MidMemoryPrice**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MinimumAllocatedMemory**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **PreAllocate**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **SessionMemoryLimit**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **WaitCountIfHighMemory**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
