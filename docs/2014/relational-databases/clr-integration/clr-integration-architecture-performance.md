---
title: CLR 통합의 성능을 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2259cf7be33fdf0e1ded99345db8102875f95618
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172207"
---
# <a name="performance-of-clr-integration"></a>통합된 CLR의 성능
  이 항목에서는의 성능을 개선할 수 있는 디자인 선택 사항 중 일부에 대해 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 와 통합은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 공용 언어 런타임 (CLR).  
  
## <a name="the-compilation-process"></a>컴파일 프로세스  
 SQL 식을 컴파일하는 중에 관리되는 루틴에 대한 참조가 발견되면 MSIL([!INCLUDE[msCoName](../../../includes/msconame-md.md)] Intermediate Language) 스텁이 생성됩니다. 이 스텁에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 CLR로의 루틴 매개 변수 마샬링, 함수 호출 및 결과 반환을 위한 코드가 포함됩니다. 이러한 "글루" 코드는 매개 변수의 형식과 매개 변수 방향(입력, 출력 또는 참조)에 기반을 둡니다.  
  
 이러한 글루 코드는 형식별 최적화를 지원하고 Null 허용 여부, 제약 패싯, 값에 의한 전달 및 표준 예외 처리와 같은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의미 체계의 효율적인 적용을 보장합니다. 인수의 정확한 형식에 맞는 코드를 생성하면 호출 경계를 넘어 형식 강제 변환이 수행되거나 boxing이라는 래퍼 개체 생성 비용이 발생하는 것을 방지할 수 있습니다.  
  
 그런 다음 생성된 스텁이 CLR의 JIT(Just-In-Time) 컴파일 서비스를 통해 네이티브 코드로 컴파일되고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 실행되고 있는 특정 하드웨어 아키텍처에 맞게 최적화됩니다. JIT 서비스는 메서드 수준에서 호출되며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 호스팅 환경이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 CLR 실행에 모두 사용할 수 있는 단일 컴파일 단위를 만들 수 있도록 지원합니다. 스텁이 컴파일되고 나면 결과 함수 포인터가 함수의 런타임 구현이 됩니다. 이러한 코드 생성 방식을 사용하면 런타임에 리플렉션이나 메타데이터 액세스와 관련된 추가 호출 비용이 발생하지 않습니다.  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>SQL Server 및 CLR 간의 빠른 전환  
 컴파일 프로세스를 수행하면 런타임에 네이티브 코드에서 호출할 수 있는 함수 포인터가 생성됩니다. 스칼라 반환 사용자 정의 함수의 경우 이 함수 호출은 행 단위로 수행됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 CLR 간의 전환 비용을 최소화하기 위해 관리되는 호출을 포함하는 문에는 대상 응용 프로그램 도메인을 확인하는 시작 단계가 있습니다. 이러한 확인 단계를 통해 각 행에서 전환 비용을 줄일 수 있습니다.  
  
## <a name="performance-considerations"></a>성능 고려 사항  
 다음 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 통합된 CLR과 관련된 성능 고려 사항에 대해 간략히 설명합니다. 더 자세한 정보를 찾을 수 있습니다 "[SQL Server 2005에서 사용 하 여 CLR 통합](http://go.microsoft.com/fwlink/?LinkId=50332)" MSDN 웹 사이트에 있습니다. 관리 코드 성능에 대 한 일반 정보를 확인할 수 있습니다 "[향상.NET 응용 프로그램 성능 및 확장성](http://go.microsoft.com/fwlink/?LinkId=50333)" MSDN 웹 사이트에 있습니다.  
  
### <a name="user-defined-functions"></a>사용자 정의 함수  
 CLR 함수는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 사용자 정의 함수보다 호출 경로가 빠르다는 장점이 있습니다. 또한 관리 코드는 프로시저 코드, 계산 및 문자열 조작 부분에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)]보다 훨씬 성능이 뛰어납니다. 계산을 많이 수행하고 데이터 액세스는 수행하지 않는 CLR 함수는 관리 코드로 작성하는 것이 좋습니다. [!INCLUDE[tsql](../../../includes/tsql-md.md)] 함수는 CLR 통합보다 데이터 액세스를 효율적으로 수행합니다.  
  
### <a name="user-defined-aggregates"></a>사용자 정의 집계  
 관리 코드는 커서 기반 집계보다 성능이 훨씬 뛰어나지만 일반적으로 기본 제공 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 집계 함수보다는 성능이 약간 떨어집니다. 네이티브 기본 제공 집계 함수가 있는 경우에는 이를 사용하는 것이 좋습니다. 필요한 집계가 기본적으로 지원되지 않는 경우에는 성능을 위해 커서 기반 구현보다는 CLR 사용자 정의 집계를 사용하는 것이 좋습니다.  
  
### <a name="streaming-table-valued-functions"></a>스트리밍 테이블 반환 함수  
 응용 프로그램에서는 함수 호출의 결과로 테이블을 반환해야 하는 경우가 많습니다. 가져오기 작업의 일부로 파일에서 표 형식 데이터를 읽거나 쉼표로 구분된 값을 관계형 표현으로 변환하는 경우를 예로 들 수 있습니다. 일반적으로 이러한 작업은 호출자가 소비하기 전에 결과 테이블을 구체화하고 채우는 방법으로 수행할 수 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 CLR이 통합됨에 따라 STVF(스트리밍 테이블 반환 함수)라는 새로운 확장성 메커니즘을 사용할 수 있게 되었습니다. 관리되는 STVF는 비슷한 기능의 확장 저장 프로시저 구현보다 성능이 우수합니다.  
  
 STVF는 `IEnumerable` 인터페이스를 반환하는 관리되는 함수입니다. `IEnumerable`에는 STVF가 반환하는 결과 집합을 탐색하는 메서드가 있습니다. STVF가 호출되면 반환된 `IEnumerable`이 쿼리 계획에 직접 연결됩니다. 쿼리 계획은 행을 인출해야 할 때 `IEnumerable` 메서드를 호출합니다. 이 반복 모델을 사용하면 전체 테이블이 채워질 때까지 기다리지 않고 첫 번째 행이 생성되면 즉시 결과를 소비할 수 있습니다. 또한 함수 호출에 소비되는 메모리 양을 크게 줄일 수 있습니다.  
  
### <a name="arrays-vs-cursors"></a>배열 및 커서  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 커서가 배열로 쉽게 표현할 수 있는 데이터를 트래버스해야 하는 경우 관리 코드를 사용하면 성능을 크게 높일 수 있습니다.  
  
### <a name="string-data"></a>문자열 데이터  
 `varchar`과 같은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문자 데이터는 관리되는 함수에서 SqlString 또는 SqlChars 형식으로 지정할 수 있습니다. SqlString 변수는 메모리에 전체 값의 인스턴스를 만듭니다. SqlChars 변수는 메모리에 전체 값의 인스턴스를 만들지 않고도 성능 및 확장성을 개선하는 데 사용할 수 있는 스트리밍 인터페이스를 제공합니다. LOB(큰 개체) 데이터의 경우 이러한 기능은 특히 중요합니다. 또한 `SqlXml.CreateReader()`에서 반환하는 스트리밍 인터페이스를 통해 서버 XML 데이터에 액세스할 수 있습니다.  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR 및 확장 저장 프로시저  
 관리되는 프로시저가 결과 집합을 클라이언트로 다시 보낼 수 있도록 지원하는 Microsoft.SqlServer.Server API(응용 프로그래밍 인터페이스)는 확장 저장 프로시저에서 사용되는 ODS(개방형 Data Services) API보다 성능이 우수합니다. 또한 System.Data.SqlServer API는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 도입된 `xml`, `varchar(max)`, `nvarchar(max)` 및 `varbinary(max)`와 같은 데이터 형식을 지원하지만 ODS API는 새로운 데이터 형식을 지원하도록 확장되지 않았습니다.  
  
 관리 코드를 사용하면 메모리, 스레드 및 동기화와 같은 리소스 사용을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 관리합니다. 이러한 리소스를 노출하는 관리되는 API가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 관리자를 기반으로 구현되기 때문입니다. 이와 달리 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 확장 저장 프로시저의 리소스 사용량을 보거나 제어할 수 없습니다. 예를 들어 확장 저장 프로시저가 CPU나 메모리 리소스를 너무 많이 소비하더라도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 이를 감지하거나 제어할 수 없습니다. 반면에 관리 코드를 사용하면 지정된 스레드가 오랫동안 양보하지 않을 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 이를 감지하여 다른 작업을 예약할 수 있도록 해당 태스크에 양보를 강요합니다. 따라서 관리 코드를 사용하면 확장성과 시스템 리소스 사용 효율이 개선됩니다.  
  
 관리 코드를 사용하면 실행 환경을 유지 관리하고 보안 검사를 수행하는 데 필요한 오버헤드가 늘어날 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내에서 실행 중이고 관리 코드와 네이티브 코드 간의 빈번한 전환이 필요한 경우가 여기에 해당합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 네이티브 코드에 진입 및 종료 시에 스레드별 설정에 대한 추가 유지 관리를 수행해야 하기 때문입니다. 따라서 관리 코드와 네이티브 코드 간의 전환이 빈번한 경우에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 내에서 실행되는 관리 코드보다 확장 저장 프로시저의 성능이 훨씬 우수합니다.  
  
> [!NOTE]  
>  확장 저장 프로시저는 더 이상 사용되지 않는 기능이므로 새로운 확장 저장 프로시저를 개발하지 않는 것이 좋습니다.  
  
### <a name="native-serialization-for-user-defined-types"></a>사용자 정의 형식에 대한 네이티브 직렬화  
 UDT(사용자 정의 형식)는 스칼라 형식 시스템을 위한 확장성 메커니즘으로 설계되었습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 `Format.Native`라는 UDT용 직렬화 형식을 구현합니다. 컴파일 중에 형식의 구조를 검사하여 해당하는 특정 형식 정의에 맞게 사용자 지정된 MSIL을 생성합니다.  
  
 네이티브 직렬화는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기본 구현입니다. 사용자 정의 직렬화는 직렬화 수행을 위해 형식 작성자가 정의한 메서드를 호출합니다. 최적의 성능을 위해 가능하면 `Format.Native` 직렬화를 사용해야 합니다.  
  
### <a name="normalization-of-comparable-udts"></a>비교할 수 있는 UDT의 정규화  
 UDT 정렬 및 비교와 같은 관계형 작업은 값의 이진 표현에 대해 직접 수행됩니다. 이러한 작업은 UDT 상태의 정규화된(이진 순서로 정렬된) 표현을 디스크에 저장하는 방식으로 이루어집니다.  
  
 정규화를 사용하면 형식 인스턴스의 생성과 메서드 호출 오버헤드를 방지하여 상당히 적은 비용으로 비교 작업을 수행할 수 있고, UDT에 대한 이진 도메인을 생성함으로써 히스토그램, 인덱스 및 형식의 값에 대한 히스토그램을 만들 수 있다는 두 가지 이점이 있습니다. 따라서 메서드 호출이 필요하지 않은 작업에서 정규화된 UDT의 성능 프로필은 네이티브 기본 제공 형식과 매우 비슷합니다.  
  
### <a name="scalable-memory-usage"></a>확장 가능한 메모리 사용  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 관리되는 가비지 수집의 원활한 수행과 확장을 위해서는 대량의 단일 할당을 피해야 합니다. 88KB보다 큰 할당은 대형 개체 힙에 배치되므로 많은 수의 작은 할당보다 가비지 수집의 성능 및 확장성이 크게 떨어집니다. 예를 들어 대형 다차원 배열을 할당해야 하는 경우에는 분산된 가변 배열로 할당하는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [CLR 사용자 정의 형식](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  