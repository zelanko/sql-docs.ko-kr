---
title: "개요 (SMO) | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
caps.latest.revision: "69"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8121a42034c748e6acd1265dee06f1552cae1cc0
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="overview-smo"></a>개요(SMO)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Management Objects (SMO)는 개체의 프로그래밍 방식으로 관리 하기 위한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. SMO를 사용하면 사용자 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 응용 프로그램을 빌드할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 관리할 수 있는 강력하고 확장성 있는 응용 프로그램이지만 SMO 응용 프로그램을 사용할 때 더 나은 결과를 얻을 수 있는 경우도 있습니다.  
  
 예를 들어 새로운 사용자의 요구 사항을 충족하고 교육 비용을 줄이기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 태스크를 제어하는 사용자 응용 프로그램을 단순하게 만들어야 하는 경우, 또는 사용자 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 만들어야 하거나 인덱스를 효율적으로 생성하고 모니터링하는 응용 프로그램을 만들어야 하는 경우 SMO 응용 프로그램을 사용할 수 있습니다. 또한 타사 하드웨어나 소프트웨어를 데이터베이스 관리 응용 프로그램에 원활하게 통합하기 위해 SMO 응용 프로그램을 사용할 수도 있습니다.  
  
 SMO는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전과 호환되므로 다중 버전 환경을 쉽게 관리할 수 있습니다.  
  
 SMO의 기능은 다음과 같습니다.  
  
-   캐시된 개체 모델 및 최적화된 개체 인스턴스 생성. 개체가 명확하게 참조될 때만 로드됩니다. 개체 속성은 개체가 만들어질 때 부분적으로 로드되며 로드되지 않은 나머지 개체와 속성은 직접 참조될 때 로드됩니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 일괄 처리 실행. 문을 일괄 처리하므로 네트워크 성능이 향상됩니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 캡처. 모든 작업을 캡처하여 스크립트로 저장할 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 이 기능을 사용하면 작업을 바로 실행하는 대신 스크립트로 만들 수 있습니다.  
  
-   WMI 공급자로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 관리. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 프로그래밍 방식으로 시작, 중지 및 일시 중지할 수 있습니다.  
  
-   고급 스크립팅. [!INCLUDE[tsql](../../includes/tsql-md.md)] 인스턴스에 다른 개체에 대한 관계를 설명하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 다시 만들기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트를 생성할 수 있습니다.  
  
-   URN(Unique Resource Names) 사용. URN을 사용하여 SMO 개체의 인스턴스를 만들거나 참조할 수 있습니다.  
  
 SMO는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 많은 기능과 구성 요소를 새 개체 또는 속성으로 나타냅니다. 이러한 새 기능과 구성 요소는 다음과 같습니다.  
  
-   파티션 구성표에 데이터를 저장하기 위한 테이블 및 인덱스 분할. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하세요.  
  
-   SOAP 요청을 관리하기 위한 HTTP 끝점. 자세한 내용은 참조 [Implementing Endpoints](../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md)합니다.  
  
-   동시성 향상을 위한 스냅숏 격리 및 행 수준 버전 관리. 자세한 내용은 참조 [스냅숏 격리 작업](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)합니다.  
  
-   XML 스키마 컬렉션, XML 인덱스 및 XML 데이터 형식으로 XML 데이터의 유효성 검사와 저장 기능 제공. 자세한 내용은 참조 [XML 스키마 컬렉션 &#40; SQL Server &#41; ](../../relational-databases/xml/xml-schema-collections-sql-server.md) 및 [XML 스키마를 사용 하 여](../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)합니다.  
  
-   데이터베이스의 읽기 전용 복사본을 만들기 위한 스냅숏 데이터베이스  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)]의 메시지 기반 통신 지원. 자세한 내용은 참조 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체의 복수 이름에 대한 동의어 지원. 자세한 내용은 참조 [동의어 &#40; 데이터베이스 엔진 &#41;](../../relational-databases/synonyms/synonyms-database-engine.md)합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전자 메일 서버, 전자 메일 프로필 및 전자 메일 계정을 생성하는 데이터베이스 메일 관리 기능. 자세한 내용은 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)을 참조하세요.  
  
-   연결 정보를 등록하기 위한 등록된 서버 지원. 자세한 내용은 참조 [서버 등록](../../tools/sql-server-management-studio/register-servers.md)합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트의 추적 및 재생. 자세한 내용은 참조 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md), [SQL 추적](../../relational-databases/sql-trace/sql-trace.md), [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md), 및 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)합니다.  
  
-   보안 제어를 위한 인증서와 키 지원. 자세한 내용은 참조 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)합니다.  
  
-   DDL 이벤트 발생 시 기능을 추가하기 위한 DDL 트리거. 자세한 내용은 [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md)을(를) 참조하세요.  
  
 SMO 네임스페이스는 <xref:Microsoft.SqlServer.Management.Smo>입니다. SMO로 구현 됩니다는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 어셈블리입니다. 즉,에서 공용 언어 런타임은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SMO 개체를 사용 하기 전에 버전 2.0을 설치 해야 합니다. 기본적으로 SMO 어셈블리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SDK 옵션과 함께 GAC(전역 어셈블리 캐시)에 설치됩니다. 어셈블리는 C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\에 배치 됩니다. 자세한 내용은 참조는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 설명서입니다.  
  
## <a name="smo-classes"></a>SMO 클래스  
 SMO 클래스에는 인스턴스 클래스 및 유틸리티 클래스라는 두 개의 범주가 포함되어 있습니다.  
  
 **인스턴스 클래스**  
  
 인스턴스 클래스는 서버, 데이터베이스, 테이블, 트리거 및 저장 프로시저와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 나타냅니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 설정하고 해당 인스턴스에 전송된 명령에 대한 캡처 모드를 제어하는 데 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스가 사용됩니다.  
  
 SMO 인스턴스 개체는 데이터베이스 서버의 계층을 나타내는 계층을 형성합니다. 이 계층의 맨 위에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 있으며 그 아래에 데이터베이스가 있고 데이터베이스 아래에 테이블, 열, 트리거 등이 있습니다. 둘 이상의 열이 있는 테이블과 같이 한 부모가 여러 자식을 갖는 논리적 관계가 있는 경우 자식은 개체 컬렉션으로 나타납니다. 그렇지 않은 경우에는 자식이 개체로만 나타납니다.  
  
 **유틸리티 클래스**  
  
 유틸리티 클래스는 특정 태스크를 수행하도록 명시적으로 생성된 개체 그룹입니다. 이러한 유틸리티 클래스는 기능에 따라 다양한 개체 계층으로 나뉩니다.  
  
-   전송 클래스. 이 클래스는 다른 데이터베이스로 스키마와 데이터를 전송하는 데 사용됩니다.  
  
-   백업 및 복원 클래스. 이러한 클래스는 데이터베이스를 백업 및 복원하는 데 사용됩니다.  
  
-   Scripter 클래스. 이 클래스는 개체와 개체의 종속성을 다시 생성하는 스크립트 파일을 만드는 데 사용됩니다.  
  
## <a name="smo-features"></a>SMO 기능  
 **최적화 된 성능**  
  
 SMO 아키텍처는 처음에 개체의 일부만 인스턴스화한 서버에서 최소한의 속성 정보만 요청 하므로 메모리 측면에서 효율적입니다. 개체를 명시적으로 참조할 때까지 개체의 전체 인스턴스화는 지연됩니다. 개체는 먼저 검색된 속성 집합에 없는 속성이 요청되었거나 그와 같은 속성을 필요로 하는 메서드가 요청될 경우에 전체적으로 인스턴스화됩니다. 부분적으로 인스턴스화된 개체와 전체적으로 인스턴스화된 개체 간의 전환은 사용자가 인식하지 못하는 사이에 이루어집니다. 또한 많은 메모리를 사용하는 일부 속성은 해당 속성이 명시적으로 참조되지 않는 한 검색되지 않습니다. 이러한 예가 <xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> 개체 속성의 <xref:Microsoft.SqlServer.Management.Smo.Database> 속성입니다. 하지만 부분 인스턴스화에는 더 많은 네트워크 왕복이 필요하므로 부분 인스턴스화가 응용 프로그램에 대한 최선의 성능 옵션이 아닐 수도 있습니다.  
  
 시스템 환경에 맞게 인스턴스화를 제어할 수 있습니다. 지연 인스턴스화를 사용하면 속성이 참조될 때 많은 서버 요청이 트리거될 수 있지만 응용 프로그램에서 필요로 하는 메모리의 양은 최소화됩니다.  
  
 실제 데이터베이스 개체를 나타내는 개체인 인스턴스 클래스는 세 가지 인스턴스화 수준에서 존재할 수 있습니다. 즉, 최소 인스턴스화(한 블록에서 최소한의 필수 속성만 읽음), 부분 인스턴스화(한 블록에서 상대적으로 많은 메모리 양을 사용하는 모든 속성을 읽음) 및 전체 인스턴스화 수준에서 존재할 수 있습니다. 인스턴스화되지 않은 상태와 전체 인스턴스화 상태가 일반적인 인스턴스화 상태입니다. 부분적으로 인스턴스화된 개체는 개체 속성 값 중 일부만 포함하므로 부분 인스턴스화 상태는 효율성을 높여 줍니다. 부분 인스턴스화는 직접 참조되지 않는 개체의 기본 상태입니다. 이러한 속성 중 하나가 참조되는 경우 개체의 전체 인스턴스화에 대한 오류 메시지가 생성됩니다.  
  
 **실행 캡처**  
  
 직접 실행이 일반적인 실행 방법입니다. 문은 문이 발생할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스로 직접 전송됩니다. 실행 캡처는 이러한 직접 전송 대신 사용되는 방식입니다.  
  
 실행 캡처를 사용하면 일반적으로 실행할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리를 캡처할 수 있습니다. 이 기능을 사용하면 SMO 프로그래머가 스크립트를 지연시키거나, 나중에 실행할 수 있도록 저장하거나, 최종 사용자에게 미리 보기를 제공할 수 있습니다. 예를 들어 **create database**, **create table**및 **create index** 문을 한 번에 전송한 다음 세 개의 순차적 단계로 실행할 수 있습니다. 이 기능은 사용자가 <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> 개체를 사용하여 제어합니다.  
  
 **WMI 공급자**  
  
 WMI 공급자 개체는 SMO로 래핑됩니다. 따라서 SMO 프로그래머는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 공급자의 네임스페이스와 세부 정보로 표현되는 프로그래밍 모델을 이해하지 못한 상태에서도 SMO 클래스와 매우 유사한 간단한 개체 모델을 사용할 수 있습니다. WMI 공급자를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 별칭, 그리고 클라이언트 및 서버 네트워크 라이브러리를 구성할 수 있습니다.  
  
 **스크립팅**  
  
 SMO에서는 스크립팅 기능이 향상되어 **Scripter** 클래스로 이전되었습니다. **Scripter** 클래스에서는 종속성을 검색하고, 개체 간의 관계를 파악하고, 종속성 계층을 조작할 수 있습니다. 기본 스크립팅 개체는 **Scripter** 개체입니다. 또한 종속성을 처리하고 진행 상태나 오류 이벤트에 응답하는 다양한 지원 개체가 있습니다.  
  
 **Scripter** 개체는 다음과 같은 고급 스크립팅 옵션을 지원합니다.  
  
-   간단한 1단계 스크립팅(1단계로 스크립트 작성)  
  
-   고급 3 단계 스크립팅 (3 단계에 따라; 스크립트를 만듭니다. 종속성 검색, 목록 생성, 스크립트 생성)  
  
-   양방향 종속성 검색(종속성 또는 종속 개체 검색 지원)  
  
-   진행률 이벤트에 응답  
  
-   오류 이벤트에 응답  
  
 **Unique Resource Names**  
  
 SMO 개체 라이브러리를 사용할 때 기반이 되는 주요 개념은 URN(Unique Resource Name)입니다. URN은 XPath와 유사한 구문을 사용합니다. XPath는 각 수준에서 한정자와 함수를 갖는 개체를 지정하는 데 사용되는 계층 경로입니다. SMO에서 URN은 경로와 제한된 기능의 특성 명명이라는 두 가지 요소를 가집니다. 경로는 개체의 위치를 지정하는 데 사용되고 특성 명명은 필터링 수준을 제어하는 데 사용됩니다.  
  
 다음은 데이터베이스에 대한 URN의 예입니다.  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 개체에 대한 URN은 URN 속성을 참조하여 검색할 수 있습니다. Scripter 개체도 **Scripter** 개체의 메서드에 개체 참조를 전달하는 매개 변수로 URN을 사용합니다. 또한 **Server** 개체의 **GetSmoObject** 메서드에 대해 URN을 지정할 수 있습니다. 이 기능을 사용하여 SMO 개체 인스턴스를 만들 수 있습니다.  
  
## <a name="sql-server-features-represented-in-smo"></a>SMO로 표현 된 SQL Server 기능  
 **테이블 및 인덱스 분**  
  
 인덱스 테이블 분할을 사용하면 파일 그룹 전체의 테이블 및 인덱스에서 데이터 분포를 관리할 수 있습니다. 이 새 기능은 SMO 개체로 표현됩니다.  
  
 **끝점**  
  
 SOAP 및 데이터베이스 미러링 요청은 <xref:Microsoft.SqlServer.Management.Smo.Endpoint> 개체를 사용하여 끝점으로 처리됩니다.  
  
 **스냅숏 격리/행 수준 버전 관리**  
  
 스냅숏 격리(행 수준 버전 관리)는 새로운 <xref:Microsoft.SqlServer.Management.Smo.Database> 개체 속성으로 표현됩니다.  
  
 **XML 스키마 Namespace, XML 인덱스 및 XML 데이터 형식**  
  
 XML 스키마 네임스페이스는 SMO에서 개체 컬렉션으로 표현됩니다. XML 인덱스는 SMO에서 **Index** 개체 속성으로 표현됩니다.  
  
 **전체 텍스트 검색의 향상 된 기능**  
  
 전체 텍스트 검색의 향상된 기능을 나타내는 새 개체가 SMO로 제공됩니다.  
  
 **페이지 확인**  
  
 <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions.PageVerify%2A> 개체는 데이터베이스 페이지 확인 옵션을 나타냅니다.  
  
 **스냅숏 데이터베이스**  
  
 스냅숏 데이터베이스는 특정 시점에 대한 지정된 데이터베이스의 읽기 전용 복사본입니다. <xref:Microsoft.SqlServer.Management.Smo.Database.IsDatabaseSnapshot%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Database> 속성을 사용하여 스냅숏 데이터베이스를 지정할 수 있습니다.  
  
 **Service Broker**  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 및 해당 기능은 개체 그룹으로 나타납니다.  
  
 **향상 된 인덱스 기능**  
  
 향상된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스 기능은 <xref:Microsoft.SqlServer.Management.Smo.Index> 개체의 새 속성으로 나타납니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
