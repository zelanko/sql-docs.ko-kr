---
title: Analysis Services 메모리 속성 | Microsoft Docs
ms.date: 03/15/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b33bf47f77d65679bc079b526d480841af71c0c4
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2019
ms.locfileid: "58072297"
---
# <a name="memory-properties"></a>메모리 속성
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Analysis Services는 사전 요청을 즉시 처리할 수 있도록 적절 한 양을 시작 메모리를 할당 합니다. 쿼리 및 처리 작업이 증가함에 따라 추가 메모리가 할당됩니다. 
  
  구성 설정을 지정하여 메모리가 해제되는 임계값을 제어할 수 있습니다. 예를 들어 **HardMemoryLimit** 설정은 더 많은 리소스를 사용할 수 있을 때까지 새로운 요청이 완전히 거부되는 자체 부과된 메모리 부족 조건을 지정합니다(기본적으로 이 임계값은 사용되지 않음).

최대 메모리 버전에서 SQL Server Analysis Services 인스턴스 당 사용량에 대 한 자세한 내용은 참조 하세요 [버전 및 SQL Server의 지원 되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)합니다.
  
 다음 설정을 설명이 없는 한 테이블 형식 및 다차원 서버에 적용 됩니다.  
 
## <a name="default-memory-configuration"></a>기본 메모리 구성

기본 구성에서 각 Analysis Services 인스턴스에 인스턴스가 유휴 상태인 경우에 시작 시 소량의 RAM (50MB로 40 MB)를 할당 합니다. 

구성 설정은 인스턴스별로 지정됩니다. 동일한 하드웨어에서 테이블 형식 및 다차원 인스턴스 등 Analysis Services의 여러 인스턴스를 실행하는 경우 각 인스턴스가 다른 인스턴스와 독립적으로 자체 메모리를 할당합니다.

아래 표에서는 자주 사용되는 메모리 설정을 간략하게 설명합니다(참조 섹션에 자세한 내용이 포함되어 있음). Analysis Services는 동일한 서버의 다른 응용 프로그램을 사용 하 여 메모리에 대 한 경쟁 하는 경우에 이러한 설정을 구성 합니다.

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
 부호 있는 64 비트 배정밀도 부동 소수점 숫자 속성 시작 되는 Analysis Services는 자주 사용된 하지 않는 캐시 등 우선 순위가 낮은 개체에 대 한 메모리를 해제 하는 첫 번째 임계값을 정의 하는입니다. 메모리가 할당되고 나면 서버에서 이 제한 아래로 메모리를 해제하지 않습니다. 기본값은 65이며 이 경우 메모리 하한은 실제 메모리 또는 가상 주소 공간의 65% 중 더 작은 쪽으로 설정됩니다.  
  
 **TotalMemoryLimit**  
 서버가 다른 요청을 위한 공간을 확보하기 위해 메모리 할당을 취소하기 시작하는 임계값을 정의합니다. 이 제한에 도달하면 인스턴스는 만료된 세션을 닫고 사용되지 않는 계산을 언로드하여 천천히 캐시 메모리를 지우기 시작합니다. 기본값은 실제 메모리 또는 가상 주소 공간의 80% 중 더 작은 쪽입니다. **TotalMemoryLimit** 는 반드시 미만 **HardMemoryLimit**  
  
 **HardMemoryLimit**  
 인스턴스가 메모리 사용량을 줄이기 위해 활성 사용자 세션을 적극적으로 종료하기 시작하는 메모리 임계값을 지정합니다. 종료 된 모든 세션에는 메모리 부족으로 취소 하는 방법에 대 한 오류가 표시 됩니다. 기본값 영(0)은 **HardMemoryLimit** 가 **TotalMemoryLimit** 와 시스템의 실제 총 메모리 사이의 중간 값으로 설정됨을 의미합니다. 시스템의 실제 메모리가 프로세스의 가상 주소 공간보다 큰 경우 **HardMemoryLimit**를 계산할 때 가상 주소 공간이 대신 사용됩니다.  

**QueryMemoryLimit**   
Azure Analysis Services에만 해당 합니다. 고급 속성을 쿼리 하는 동안 임시 결과에서 얼마나 많은 메모리를 사용할 수 있습니다. DAX 측정값 및 쿼리에만 적용 됩니다. 쿼리에 사용 되는 일반 메모리 할당에 고려 되지 않습니다. 최대 100%에서를 지정 합니다. 그 외에도 바이트입니다. 지정 된 설정 값이 0 이면 제한이 없습니다. Azure 분석에 대 한 기본값은 계획에 의해 결정 됩니다. 

|계획  |Default  |
|---------|---------|
|D1     |   80      |
|다른 모든 계획     |    20     | 

 **VirtualMemoryLimit**  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **VertiPaqPagingPolicy**  
  테이블 형식 인스턴스에만 적용되며, 서버의 메모리가 부족한 경우에 발생하는 페이징 동작을 지정합니다. 유효한 값은 다음과 같습니다.  
  
설정  |Description  
---------|---------
**0**     |  (Azure Analysis Services에 대 한 기본값) 페이징 하는 사용 하지 않도록 설정 합니다. 메모리가 부족하면 메모리 부족 오류로 처리가 실패합니다. 페이징을 사용하지 않도록 설정한 경우 서비스 계정에 대한 권한을 Windows에 부여해야 합니다. 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)을 참조하세요. 
**1**     |  (SQL Server Analysis Services에 대 한 기본값) 이 속성에는 하는 운영 체제 페이지 파일 (pagefile.sys)을 사용 하 여 디스크로 페이징이 발생할을 수 있습니다.   
  
1로 설정될 경우 서버는 지정된 방법을 사용하여 디스크로 페이징을 시도하기 때문에 메모리 제약 조건으로 인해 처리가 실패할 가능성이 적습니다. **VertiPaqPagingPolicy** 속성을 설정한다고 해서 메모리 오류가 절대로 발생하지 않는 것은 아닙니다. 다음과 같은 상황에서 메모리 부족 오류가 여전히 발생할 수 있습니다.  
  
-   모든 사전에 대해 메모리가 충분하지 않습니다. 서버 메모리의 각 열에 대해 사전을 잠그며 처리 중 이며 지정 된 값 보다 더 많은 일 수 없습니다 모든 합 **VertiPaqMemoryLimit**합니다.  
  
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
**5** | 하이브리드 할당자. 이 할당자에 대 한 Windows LFH 사용할지 \<16kb 및 AS 힙을 = > 16kb입니다. 
**6** | Intel TBB 할당자. SQL Server 2016 SP1 이상 Analysis Services에서 사용할 수 있습니다.
  
  
 **HeapTypeForObjects**  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다. 유효한 값은 다음과 같습니다.
  
   설정 | Description
--------|------------
**-1** | (기본값) 자동. 사용할 항목을 엔진이 결정합니다.
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
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
