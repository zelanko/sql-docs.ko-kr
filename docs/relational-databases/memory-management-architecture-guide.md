---
title: "메모리 관리 아키텍처 가이드 | Microsoft 문서"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, memory management architecture
- memory management architecture guide
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d00e5c97e6c27f3fe40b2066b5e194b8011f6b1e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="memory-management-architecture-guide"></a>메모리 관리 아키텍처 가이드
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

## <a name="memory-architecture"></a>메모리 아키텍처

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 메모리를 필요에 따라 동적으로 확보하고 해제합니다. 일반적으로 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 할당해야 하는 메모리의 양을 지정할 필요가 없습니다. 해당 옵션이 계속 유지되고 일부 환경에서는 필요할 경우에도 마찬가지입니다.

디스크 읽기 및 쓰기가 리소스를 가장 많이 소모하는 작업이기 때문에 모든 데이터베이스 소프트웨어의 주요 설계 목표 중 하나는 디스크 입/출력을 최소화하는 것입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 데이터베이스에서 읽은 페이지를 보관하도록 메모리에 버퍼 풀을 만듭니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 코드 중 상당수가 디스크와 버퍼 풀 간의 물리적 읽기 횟수와 쓰기 횟수를 최소화하는 데 사용됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 다음 두 가지 목표를 균형 있게 유지하려고 합니다.

* 전체 시스템의 메모리가 부족해지지 않도록 적정한 수준의 버퍼 풀 크기 유지
* 버퍼 풀의 크기를 최대화하여 데이터베이스 파일에 대한 실제 입출력 최소화


> [!NOTE]
> 사용량이 많은 시스템에서는 많은 메모리가 필요한 일부 대규모 쿼리를 실행하는 경우 요청한 최소 메모리 용량을 얻지 못하고 메모리 리소스를 대기하는 동안 시간 초과 오류가 발생하게 됩니다. 이 문제를 해결하려면 [query wait 옵션](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md)을 늘립니다. 병렬 쿼리의 경우 [max degree of parallelism 옵션](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)을 줄여 보세요.
 
> [!NOTE]
> 사용량이 많고 메모리가 부족한 시스템에서는 쿼리가 비트맵에 필요한 최소 메모리를 얻지 못할 경우 쿼리 계획에 병합 조인, 정렬 및 비트맵이 포함된 쿼리에서 비트맵을 삭제할 수 있습니다. 이 경우 쿼리 성능에 영향을 줄 수 있으며 정렬 프로세스가 메모리에 들어가지 않을 경우 tempdb 데이터베이스의 작업 테이블 사용이 증가하여 tempdb가 확장될 수 있습니다. 이 문제를 해결하려면 실제 메모리를 추가하거나 더 빠른 다른 쿼리 계획을 사용하도록 쿼리를 튜닝합니다.
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 최대 메모리 양 제공

AWE와 Lock Pages in Memory 권한을 사용하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진에 다음과 같이 메모리 양을 제공할 수 있습니다. 다음 표에는 이제 사용할 수 없는 32비트 버전의 열이 나와 있습니다.

| |32비트 <sup>1</sup> |64비트
|-------|-------|-------| 
|기본 메모리 |모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전 프로세스 가상 주소 공간 제한까지 허용됩니다. <br>- 2GB<br>- 3 GB /3gb 부팅 매개 변수를 사용하면 3GB <sup>2</sup> <br>- WOW64에서는 4GB <sup>3</sup> |모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전 프로세스 가상 주소 공간 제한까지 허용됩니다. <br>- IA64 아키텍처에서는 7TB(IA64는 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 이상에서 지원되지 않음)<br>- 최대 x64 아키텍처의 운영 체제가 지원하는 최대 크기 <sup>4</sup>
|AWE 메커니즘( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 32비트 플랫폼의 프로세스 가상 주소 공간 제한을 초과할 수 있도록 허용) |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard, Enterprise 및 개발자 버전: 버퍼 풀에서 최대 64GB의 메모리에 액세스할 수 있습니다.|해당 사항 없음 <sup>5</sup> |
|메모리의 페이지 잠금 운영 체제(OS) 권한(실제 메모리 잠금을 허용하여 잠긴 메모리의 OS 페이징 방지) <sup>6</sup> |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard, Enterprise 및 개발자 버전: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로세스에서 AWE 메커니즘을 사용하려면 필요합니다. AWE 메커니즘을 통해 할당된 메모리는 페이징할 수 없습니다. <br> AWE를 사용하지 않고 이 권한을 부여하면 서버에 영향을 주지 않습니다. |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 및 개발자 버전: 운영 체제 페이징 방지를 위해 권장됩니다. 작업에 따라 성능이 향상될 수 있습니다. 액세스할 수 있는 메모리 양은 기본 메모리의 경우와 유사합니다. |

<sup>1</sup> 32비트 버전은 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]부터 사용할 수 없습니다.  
<sup>2</sup> /3gb는 운영 체제 부팅 매개 변수입니다. 자세한 내용은 MSDN 라이브러리를 참조하세요.  
<sup>3</sup> WOW64(Windows on Windows 64)는 32비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 64비트 운영 체제에서 실행되는 모드입니다.  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition supports up to 128 GB. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition은 운영 체제가 지원하는 최대 크기를 지원합니다.  
<sup>5</sup> sp_configure awe enabled 옵션은 64비트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 있지만 무시됩니다.    
<sup>6</sup> 32비트에서 AWE 지원에 대해 또는 64비트에서 단독으로 LPIM(메모리의 페이지 잠금) 권한이 부여된 경우 max server memory도 설정하는 것이 좋습니다.

> [!NOTE]
> 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 32비트 운영 체제에서 실행할 수 있었습니다. 32비트 운영 체제에서 4GB가 넘는 메모리에 액세스하려면 AWE(Address Windowing Extension)에서 메모리를 관리해야 합니다. 이는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 64비트 운영 체제에서 실행할 경우에는 필요하지 않습니다. AWE에 대한 자세한 내용은 [2008 설명서에서](https://msdn.microsoft.com/library/ms189334) 프로세스 주소 공간 [및](https://msdn.microsoft.com/library/ms191481) 큰 데이터베이스의 메모리 관리 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 참조하세요.   


## <a name="dynamic-memory-management"></a>동적 메모리 관리

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진의 기본 메모리 관리 동작은 시스템에 메모리가 부족해지지 않도록 필요한 만큼 메모리를 확보하는 것입니다. 데이터베이스 엔진은 Microsoft Windows의 메모리 알림 API를 사용하여 이 작업을 수행합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 가상 주소 공간은 두 개의 고유 영역으로 나눌 수 있는데, 버퍼 풀에 사용되는 공간과 그 나머지에 사용되는 공간이 그것입니다. AWE 메커니즘을 사용하면 버퍼 풀이 AWE 매핑된 메모리에 있을 수 있으며 데이터베이스 페이지를 위한 추가 공간을 제공합니다. 

버퍼 풀은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 주 메모리 할당 원본으로 사용됩니다. COM 개체 등 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로세스에 있으며 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 메모리 관리 기능을 인식하지 못하는 외부 구성 요소는 버퍼 풀이 차지하는 가상 주소 공간 밖에 있는 메모리를 사용합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 시작되면 시스템에 있는 실제 메모리 양 등의 여러 매개 변수, 서버 스레드 수 및 다양한 시작 매개 변수를 기준으로 버퍼 풀의 가상 주소 공간 크기를 계산합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 버퍼 풀에 사용할 해당 프로세스 가상 주소 공간 크기를 계산하여 예약하지만 현재 로드에 필요한 실제 메모리 양만 확보합니다(커밋).

그런 다음 인스턴스가 작업을 지원하는 데 필요한 메모리를 계속 확보합니다. 더 많은 사용자가 연결하여 쿼리를 실행하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 필요할 때마다 실제 메모리를 더 확보합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스는 max server memory 할당 목표량에 도달하거나 Windows에서 더 이상 여유 메모리가 없다고 표시할 때까지 실제 메모리를 계속 확보합니다. min server memory 설정보다 메모리가 많거나 Windows에서 사용 가능한 메모리가 부족하다고 표시하면 메모리를 해제합니다.

다른 응용 프로그램은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스를 실행 중인 컴퓨터에서 시작될 때 메모리를 소비하므로 사용 가능한 실제 메모리 양이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 목표량 아래로 떨어집니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 메모리 소비를 조정합니다. 다른 응용 프로그램이 중지되어 가용 메모리가 늘어나면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 인스턴스가 메모리 할당량을 늘립니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 초 단위로 몇 MB의 메모리를 해제하고 확보하기 때문에 메모리 할당량 변화에 따라 빠르게 조정됩니다.


## <a name="effects-of-min-and-max-server-memory"></a>min 및 max server memory의 효과

min server memory 및 max server memory 구성 옵션은 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진의 버퍼 풀에서 사용하는 메모리 양의 상한 및 하한을 설정합니다. 버퍼 풀은 min server memory에 지정된 메모리의 양을 즉시 확보하지 않습니다. 버퍼 풀은 초기화하는 데 필요한 메모리만으로 시작합니다. 데이터베이스 엔진 작업이 증가할 때 버퍼 풀에서는 작업을 지원하는 데 필요한 메모리를 계속 확보합니다. 버퍼 풀은 min server memory에 지정된 양에 도달할 때까지 확보한 메모리를 해제하지 않습니다. min server memory에 도달하면 버퍼 풀은 표준 알고리즘을 사용하여 필요할 때 메모리를 확보하고 해제합니다. 유일한 차이점은 버퍼 풀이 min server memory에 지정된 수준 아래로 메모리 할당량을 떨어뜨리지 않고 max server memory에 지정된 수준보다 더 많은 메모리를 절대로 확보하지 않는다는 것입니다.

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 프로세스로서 max server memory 옵션이 지정한 것 보다 더 많은 메모리를 확보합니다. 내부 및 외부 구성 요소 모두 추가 메모리를 사용하는 버퍼 풀 외부로 메모리를 할당할 수 있지만 일반적으로 버퍼 풀에 할당된 메모리가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용하는 메모리의 가장 큰 부분을 차지합니다.


데이터베이스 엔진에서 확보한 메모리 양은 인스턴스에 배치된 작업에 따라 완전히 달라집니다. 많은 요청을 처리하지 않은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스는 min server memory에 절대로 도달할 수 없습니다.

min server memory 및 max server memory 둘 모두에 같은 값이 지정된 경우 데이터베이스 엔진에 할당된 메모리가 해당 값에 도달하면 데이터베이스 엔진은 버퍼 풀에 대한 메모리의 동적 해제 및 확보를 중지합니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 다른 응용 프로그램이 자주 중지되거나 시작되는 컴퓨터에서 실행 중인 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 의한 메모리 할당 및 할당 취소는 다른 응용 프로그램의 시작 시간을 늦출 수 있습니다. 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 단일 컴퓨터에서 실행되는 여러 서버 응용 프로그램 중 하나인 경우 시스템 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 할당된 메모리 양을 제어해야 할 수도 있습니다. 이러한 경우 min server memory 및 max server memory 옵션을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 사용할 수 있는 메모리 양을 제어할 수 있습니다. 자세한 내용은 [Server Memory Configuration Options](../database-engine/configure-windows/server-memory-server-configuration-options.md)(서버 메모리 구성 옵션)를 참고하세요.

min server memory 및 max server memory 옵션은 MB 단위로 지정됩니다.

## <a name="memory-used-by-includessnoversionincludesssnoversion-mdmd-objects-specifications"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체 사양에서 사용하는 메모리

다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 다양한 개체에서 사용하는 대략적인 메모리 양을 설명합니다. 제시된 크기는 추정값이기 때문에 사용 중인 환경과 개체 생성 방법에 따라 다를 수 있습니다.

* 잠금: 64바이트+32바이트(소유자당)   
* 사용자 연결: 약 (3* *network_packet_size + 94KB)    

네트워크 패킷 크기는 응용 프로그램과 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진 간의 통신에 사용하는 TDS(Tabular Data Stream) 패킷의 크기입니다. 기본 패킷 크기는 4KB이며 네트워크 패킷 크기 구성 옵션으로 제어됩니다.

다중 활성 결과 집합(MARS)을 사용할 수 있으면 사용자 연결은 약 (3 + 3 * num_logical_connections) * network_packet_size + 94KB입니다.

## <a name="buffer-management"></a>버퍼 관리

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 주 목적은 데이터 저장 및 검색이므로 데이터베이스 엔진의 핵심 특성은 집중형 디스크 I/O입니다. 디스크 I/O 작업은 많은 리소스를 소비하며 완료하는 데 비교적 오랜 시간이 걸리므로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서는 I/O의 효율성을 높이는 데 주안점을 둡니다. 버퍼 관리는 이러한 효율성을 얻기 위한 핵심 구성 요소입니다. 버퍼 관리 구성 요소는 데이터베이스 페이지에 액세스하고 업데이트하기 위한 버퍼 관리자와 데이터베이스 파일 I/O를 줄이기 위한 버퍼 캐시(버퍼 풀이라고도 함)의 두 가지 메커니즘으로 구성되어 있습니다. 

### <a name="how-buffer-management-works"></a>버퍼 관리 작업 방법

버퍼는 데이터 또는 인덱스 페이지와 같은 크기인 8KB 메모리 페이지입니다. 따라서 버퍼 캐시는 8KB 페이지로 나누어집니다. 버퍼 관리자는 데이터 또는 인덱스 페이지를 데이터베이스 디스크 파일에서 버퍼 캐시로 읽어 오고 수정한 페이지를 디스크에 다시 쓰는 기능을 관리합니다. 페이지는 버퍼 관리자에 더 많은 데이터를 읽어 올 버퍼 영역이 필요할 때까지 버퍼 캐시에 남아 있습니다. 데이터는 수정되는 경우에만 다시 디스크에 쓰여집니다. 버퍼 캐시의 데이터는 여러 번 수정한 후 디스크에 다시 쓸 수 있습니다. 자세한 내용은 [페이지 읽기](../relational-databases/reading-pages.md) 및 [페이지 쓰기](../relational-databases/writing-pages.md)를 참조하세요.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 가 시작되면 시스템에 있는 실제 메모리 크기, 구성된 서버 스레드 개수, 다양한 시작 매개 변수 등 여러 매개 변수를 기준으로 버퍼 캐시의 가상 주소 공간 크기를 계산합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 버퍼 캐시에 사용할 해당 프로세스 가상 주소 공간(메모리 대상이라고도 함) 크기를 계산하여 예약하지만 현재 로드에 필요한 실제 메모리 양만 확보합니다(커밋). **sys.dm_os_sys_info** 카탈로그 뷰에서 **bpool_commit_target** 및 [bpool_committed columns](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) 열을 쿼리하여 메모리 대상으로 예약된 페이지 수와 버퍼 캐시에 현재 커밋된 페이지 수를 각각 반환할 수 있습니다.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 시작 시간과 버퍼 캐시가 해당 메모리 대상을 확보하는 시간 사이의 간격을 램프 업(ramp-up)이라고 합니다. 이 시간 동안 필요에 따라 읽기 요청이 버퍼를 채웁니다. 예를 들어 단일 페이지 읽기 요청은 단일 버퍼 페이지를 채웁니다. 즉, 램프 업은 클라이언트 요청의 개수 및 유형에 따라 달라집니다. 단일 페이지 읽기 요청을 정렬된 8페이지 요청으로 변환하여 램프 업을 신속히 처리합니다. 이를 통해 메모리가 많은 컴퓨터에서 특히 램프 업이 더 빠르게 완료될 수 있습니다.

버퍼 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로세스에서 대부분의 메모리를 사용하므로 메모리 관리자와 협력하여 다른 구성 요소가 해당 버퍼를 사용할 수 있도록 합니다. 버퍼 관리자는 다음 구성 요소와 주로 상호 작용합니다.

* 전체 메모리 사용량을 제어하며 32비트 플랫폼에서 주소 공간 사용량을 제어하는 리소스 관리자  
* 하위 수준 파일 I/O 작업을 위한 SQLOS( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 운영 체제) 및 데이터베이스 관리자  
* 미리 쓰기 로깅을 위한 로그 관리자  

### <a name="supported-features"></a>지원되는 기능

버퍼 관리자는 다음과 같은 기능을 지원합니다.

* 버퍼 관리자는 NUMA(Non-Uniform Memory Access)를 인식합니다. 버퍼 캐시 페이지는 하드웨어 NUMA 노드에 분산되므로 스레드가 외부 메모리 대신 로컬 NUMA 노드에 할당된 버퍼 페이지에 액세스할 수 있습니다. 
* 버퍼 관리자는 Hot Add 메모리를 지원하므로 사용자가 서버를 다시 시작하지 않고도 실제 메모리를 추가할 수 있습니다. 
* 버퍼 관리자는 64비트 플랫폼에서 큰 페이지를 지원합니다. 페이지 크기는 Windows 버전에 따라 달라집니다. 
* 버퍼 관리자는 동적 관리 뷰를 통해 표시되는 추가 진단 기능을 제공합니다. 이러한 뷰를 사용하여 다양한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]관련 운영 체제 리소스를 모니터링할 수 있습니다. 예를 들어 sys.dm_os_buffer_descriptors 뷰를 사용하여 버퍼 캐시의 페이지를 모니터링할 수 있습니다.   

### <a name="disk-io"></a>디스크 I/O
버퍼 관리자는 데이터베이스에 대해 읽기 및 쓰기만 수행합니다. 열기, 닫기, 확장, 축소와 같은 기타 파일 및 데이터베이스 작업은 데이터베이스 관리자 및 파일 관리자 구성 요소에 의해 수행됩니다. 

버퍼 관리자가 수행하는 디스크 I/O 작업의 특성은 다음과 같습니다.

* 모든 I/O가 비동기적으로 수행되므로 I/O 작업이 백그라운드에서 수행되는 동안 호출한 스레드는 처리를 계속할 수 있습니다.
* affinity I/O 옵션을 사용하지 않는 한 모든 I/O는 호출한 스레드에서 실행됩니다. affinity I/O mask 옵션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 디스크 I/O를 지정된 CPU 하위 집합에 바인딩합니다. 고성능 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] OLTP(온라인 트랜잭션 처리) 환경에서 이러한 확장을 통해 I/O를 실행하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 스레드의 성능을 향상시킬 수 있습니다.
* 다중 페이지 I/O는 분산 수집 I/O로 수행되므로 데이터를 인접하지 않은 메모리 영역으로 또는 이러한 영역 밖으로 전송할 수 있습니다. 이를 통해 여러 실제 I/O 요청을 피하면서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 버퍼 캐시를 신속하게 채우거나 플러시할 수 있습니다. 

#### <a name="long-io-requests"></a>긴 I/O 요청  
버퍼 관리자는 15초 이상 보류 상태에 있는 모든 I/O 요청을 보고합니다. 이를 통해 시스템 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 문제와 I/O 하위 시스템 문제를 구분할 수 있습니다. 다음과 같이 오류 메시지 833이 보고되어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 오류 로그에 나타납니다.

`` 
SQL Server has encountered %d occurrence(s) of I/O requests taking longer than %d seconds to complete on file [%ls] in database [%ls] (%d). The OS file handle is 0x%p. The offset of the latest long I/O is: %#016I64x.
`` 

긴 I/O는 읽기 또는 쓰기일 수 있으나 현재 이러한 정보는 메시지에 나타나 있지 않습니다. 긴 I/O 메시지는 오류가 아니라 경고입니다. 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]관련 문제를 나타내지 않습니다. 시스템 관리자는 보고되는 메시지를 통해 느린 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 응답 시간의 원인을 보다 빨리 찾고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]제어를 벗어난 문제를 구분할 수 있습니다. 해당 메시지를 받는다고 해서 특별한 동작을 수행해야 하는 것은 아니지만 시스템 관리자는 I/O 요청이 오래 걸리는 이유와 그러한 지연에 적합한 이유가 있는지 여부를 조사해야 합니다.

#### <a name="causes-of-long-io-requests"></a>긴 I/O 요청의 원인  
긴 I/O 메시지는 I/O가 영구적으로 차단되어 완료될 수 없거나(손실된 I/O) 단순히 아직 완료되지 않았음을 나타냅니다. 손실된 I/O로 인해 래치 제한 시간이 초과되는 경우가 많기는 하지만 메시지를 통해 어떤 시나리오가 이 경우에 해당하는지 알 수는 없습니다.

긴 I/O는 디스크 하위 시스템에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작업이 너무 많이 집중되어 있음을 나타냅니다. 다음과 같은 경우 디스크 하위 시스템이 부적절한 상태에 있다는 메시지가 나타날 수 있습니다.

* 많은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작업을 수행하는 동안 여러 개의 긴 I/O 메시지가 오류 로그에 나타나는 경우
* Perfmon 카운터가 긴 디스크 지연 시간, 긴 디스크 큐 또는 디스크 유휴 시간 없음을 표시하는 경우  

디스크 헤드의 현재 위치에 더 가까이 있는 새로운 요청을 처리하기 위해 이전 I/O 요청 처리를 계속 연기하는 I/O 경로의 구성 요소(예: 드라이버, 컨트롤러 또는 펌웨어)로 인해 긴 I/O가 발생할 수도 있습니다. 읽기/쓰기 헤드의 현재 위치에 가장 가까운 요청을 우선적으로 처리하는 방법을 "엘리베이터 검색"이라고 합니다. 대부분의 I/O가 즉시 처리되므로 Windows 시스템 모니터 도구(PERFMON.EXE)로 이를 확인하는 것은 어려울 수 있습니다. 긴 I/O 요청은 백업과 복원, 테이블 검색, 정렬, 인덱스 생성, 대량 로드, 파일 비우기와 같은 순차 I/O를 대량으로 수행하는 작업으로 인해 악화될 수 있습니다.

위에 나열된 어떤 조건과도 관련되지 않은 격리된 긴 I/O는 하드웨어 또는 드라이버 문제로 인해 발생할 수 있습니다. 시스템 이벤트 로그에 문제를 진단하는 데 도움이 되는 관련 이벤트가 포함되어 있을 수 있습니다.

#### <a name="error-detection"></a>오류 검색  
데이터베이스 페이지는 페이지를 디스크에 쓸 때부터 다시 읽을 때까지의 페이지 무결성을 보장하는 두 가지 선택적 메커니즘인 조각난 페이지 보호와 체크섬 보호 중 하나를 사용할 수 있습니다. 이러한 메커니즘을 사용하면 데이터 저장소뿐만 아니라 컨트롤러, 드라이버, 케이블, 심지어는 운영 체제를 비롯한 하드웨어 구성 요소의 정확성을 확인하는 독자적인 방법을 활용할 수 있습니다. 이러한 보호는 페이지를 디스크에 쓰기 바로 전에 페이지에 추가되며 디스크에서 읽은 후 확인됩니다.

#### <a name="torn-page-protection"></a>조각난 페이지 보호  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000에 도입된 조각난 페이지 보호는 주로 전원 오류로 인한 페이지 손상을 검색하는 방법입니다. 예를 들어 예기치 않은 전원 오류로 인해 페이지의 일부만 디스크에 쓰일 수 있습니다. 조각난 페이지 보호를 사용하면 원래의 2비트가 페이지 머리글로 복사된 후 페이지의 각 512바이트 구역 끝에 2비트 서명이 저장됩니다. 매 쓰기 작업 시 서명에 이진 01과 이진 10이 번갈아 사용되기 때문에 섹터의 일부분만 디스크에 기록되는 경우가 있으면 빠짐없이 이를 알려줍니다. 나중에 페이지를 읽을 때 비트가 잘못된 상태이면 페이지가 잘못 작성된 것이며 조각난 페이지가 검색됩니다. 조각난 페이지 검색은 최소한의 리소스를 사용하지만 디스크 하드웨어 오류로 인한 모든 오류를 검색하지는 않습니다.

#### <a name="checksum-protection"></a>체크섬 보호  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005에 도입된 체크섬 보호는 보다 강력한 데이터 무결성 검사 기능을 제공합니다. 체크섬은 쓰인 각 페이지의 데이터에 대해 계산되어 페이지 머리글에 저장됩니다. 저장된 체크섬이 있는 페이지를 디스크에서 읽을 때마다 데이터베이스 엔진은 페이지의 데이터에 대한 체크섬을 다시 계산하고 새 체크섬이 저장된 체크섬과 다를 경우 오류 824를 발생시킵니다. 체크섬 보호는 페이지의 모든 바이트에 의해 영향을 받으므로 조각난 페이지 보호보다 더 많은 오류를 catch할 수 있지만 많은 리소스를 소비합니다. 체크섬을 설정하면 버퍼 관리자가 디스크에서 페이지를 읽을 때마다 전원 오류 및 결함이 있는 하드웨어나 펌웨어로 인한 오류를 검색할 수 있습니다.

사용되는 페이지 보호 유형은 페이지를 포함하는 데이터베이스의 특성입니다. 체크섬 보호는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 이상 버전에서 생성된 데이터베이스의 기본 보호 메커니즘입니다. 페이지 보호 메커니즘은 데이터베이스 생성 시 지정하며 ALTER DATABASE를 사용하여 변경할 수 있습니다. [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰의 page_verify_option 열 또는 [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md) 함수의 IsTornPageDetectionEnabled 속성을 쿼리하여 현재 페이지 보호 설정을 확인할 수 있습니다. 페이지 보호 설정을 변경해도 새 설정이 전체 데이터베이스에 즉시 영향을 주지는 않습니다. 대신 페이지는 다음에 쓰일 때부터 데이터베이스의 현재 보호 수준을 적용합니다. 이에 따라 데이터베이스가 보호 유형이 서로 다른 여러 페이지로 구성될 수 있습니다. 

## <a name="understanding-non-uniform-memory-access"></a>NUMA(Non-Uniform Memory Access) 이해

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 NUMA(Non-Uniform Memory Access)를 인식하며 특수한 구성 없이 NUMA 하드웨어에서 원활하게 작동합니다. 클럭 속도와 프로세서 수가 증가할수록 이러한 추가 처리 능력을 사용하는 데 필요한 메모리 대기 시간을 줄이기가 더 어려워집니다. 이러한 문제를 피하기 위해 하드웨어 공급업체에서는 대용량의 L3 캐시를 제공하지만 이는 제한적인 해결책입니다. NUMA 아키텍처는 확장성 있는 솔루션으로 이 문제를 해결합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 응용 프로그램을 변경할 필요 없이 NUMA 기반 컴퓨터를 활용하도록 설계되었습니다. 자세한 내용은 [방법: 소프트 NUMA를 사용하도록 SQL Server 구성](../database-engine/configure-windows/soft-numa-sql-server.md)을 참조하세요.

## <a name="see-also"></a>관련 항목:
[페이지 읽기](../relational-databases/reading-pages.md)   
 [페이지 쓰기](../relational-databases/writing-pages.md)


