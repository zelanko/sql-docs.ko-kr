---
title: 데이터베이스 엔진 인스턴스(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2e38b572535011737f33ba1e4c438540ecdd6849
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811234"
---
# <a name="database-engine-instances-sql-server"></a>데이터베이스 엔진 인스턴스(SQL Server)
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 운영 체제 서비스로 실행되는 `sqlservr.exe` 실행 파일의 복사본입니다. 각 인스턴스는 여러 시스템 데이터베이스와 하나 이상의 사용자 데이터베이스를 관리합니다. 각 컴퓨터에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 여러 인스턴스를 실행할 수 있습니다. 애플리케이션은 인스턴스가 관리하는 데이터베이스에서 작업을 수행하기 위해 인스턴스에 연결합니다.  
  
## <a name="instances"></a>인스턴스  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 해당 인스턴스에서 관리하는 데이터베이스에 있는 데이터에 대한 응용 프로그램의 모든 작업 요청을 처리하는 서비스로 작동되며, 애플리케이션에서 보내는 연결 요청 (로그인)의 대상이 됩니다. 애플리케이션과 인스턴스가 개별 컴퓨터에 있는 경우 연결은 네트워크 연결을 통해 실행됩니다. 애플리케이션과 인스턴스가 동일한 컴퓨터에 있는 경우 SQL Server 연결은 네트워크 연결 또는 메모리 내 연결로 실행될 수 있습니다. 연결이 완료되면 애플리케이션은 해당 연결을 통해 인스턴스에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 보냅니다. 인스턴스는 데이터베이스의 데이터 및 개체를 기준으로 작업에 대한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 확인한 후 로그인 자격 증명에 필요한 권한이 부여되어 있는 경우 작업을 수행합니다. 모든 검색된 데이터는 오류 메시지 등과 함께 애플리케이션에 반환됩니다.  
  
 같은 컴퓨터에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 여러 인스턴스를 실행할 수 있습니다. 하나의 인스턴스가 기본 인스턴스가 될 수 있습니다. 기본 인스턴스는 이름이 없습니다. 연결 요청에 컴퓨터 이름만 지정된 경우 기본 인스턴스에 연결합니다. 인스턴스를 설치할 때 이름을 지정하는 인스턴스가 명명된 인스턴스입니다. 인스턴스에 연결하려면 연결 요청에서 컴퓨터 이름과 인스턴스 이름을 모두 지정해야 합니다. 기본 인스턴스를 설치할 경우 별도의 요구 사항이 없습니다. 컴퓨터에서 실행 중인 모든 인스턴스는 명명된 인스턴스가 될 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|인스턴스의 속성을 구성하는 방법에 대해 설명합니다. 파일 위치, 날짜 형식 등과 같은 기본값을 구성하거나, 인스턴스에서 운영 체제 리소스(예: 메모리, 스레드 등)를 사용하는 방법을 구성합니다.|[데이터베이스 엔진 인스턴스 구성&#40;SQL Server&#41;](database-engine-instances-sql-server.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 대한 데이터 정렬을 구성하는 방법에 대해 설명합니다. 데이터 정렬에서는 문자를 표시하는 데 사용되는 비트 패턴과 관련 동작(예: 정렬, 비교 작업의 대/소문자 또는 악센트 구분 등)을 정의합니다.|[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)|  
|OLE DB 데이터 원본에 저장된 데이터를 사용하기 위해 인스턴스에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있도록 연결된 서버 정의를 구성하는 방법에 대해 설명합니다.|[연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|로그온 시도를 확인한 후 인스턴스에서 리소스 작업을 시작하기 이전에 수행할 동작을 지정하는 LOGON 트리거를 생성하는 방법에 대해 설명합니다. LOGON 트리거는 동작(예: 연결 활동 기록, Windows 및 SQL Server에서 수행되는 자격 증명 인증과 논리를 기반으로 로그인 제한)을 지원합니다.|[LOGON 트리거](../../relational-databases/triggers/logon-triggers.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스와 연결된 서비스를 관리하는 방법에 대해 설명합니다. 여기에는 서비스 시작 및 중지, 시작 옵션 구성 등과 같은 동작이 포함됩니다.|[데이터베이스 엔진 서비스 관리](manage-the-database-engine-services.md)|  
|프로토콜 설정, 프로토콜에서 사용하는 포트 또는 파이프 수정, 암호화 구성, SQL Server Browser 서비스 구성, 네트워크에서 SQL Server 데이터베이스 엔진 표시 또는 숨김 및 서버 보안 주체 이름 등록과 같은 서버 네트워크 구성 태스크를 수행하는 방법에 대해 설명합니다.|[서버 네트워크 구성](server-network-configuration.md)|  
|클라이언트 프로토콜 구성 및 만들기 또는 서버 별칭 삭제와 같은 클라이언트 네트워크 구성 태스크를 수행하는 방법에 대해 설명합니다.|[클라이언트 네트워크 구성](client-network-configuration.md)|  
|스크립트(예: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스크립트)를 디자인, 디버깅 및 실행하는 데 사용할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 편집기에 대해 설명합니다. 또한 SQL Server 구성 요소 작업을 위해 Windows PowerShell 스크립트를 코딩하는 방법에 대해 설명합니다.|[데이터베이스 엔진 스크립팅](../../relational-databases/scripting/database-engine-scripting.md)|  
|유지 관리 계획을 사용하여 인스턴스에 대한 일반 관리 태스크 워크플로를 지정하는 방법에 대해 설명합니다. 워크플로에는 성능 향상을 위한 데이터베이스 백업, 통계 업데이트 등과 같은 태스크가 포함됩니다.|[유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|리소스 관리자를 통해 애플리케이션 요청에 사용할 수 있는 CPU 및 메모리의 양을 제한하여 리소스 소비와 작업을 관리하는 방법에 대해 설명합니다.|[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)|  
|데이터베이스 애플리케이션에서 데이터베이스 메일을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]로부터 전자 메일 메시지를 보내는 방법에 대해 설명합니다.|[데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)|  
|확장 이벤트를 사용하여 성능 기준을 작성하거나 성능 문제를 진단하는 데 사용할 수 있는 성능 데이터를 캡처하는 방법에 대해 설명합니다. 확장 이벤트는 성능 데이터 수집을 위한 경량형의 확장성이 뛰어난 시스템입니다.|[확장 이벤트](../../relational-databases/extended-events/extended-events.md)|  
|SQL 추적을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 이벤트 캡처 및 기록을 위한 사용자 지정 시스템을 작성하는 방법에 대해 설명합니다.|[SQL 추적](../../relational-databases/sql-trace/sql-trace.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로파일러를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스로 들어오는 응용 프로그램 요청 추적을 캡처하는 방법에 대해 설명합니다. 나중에 성능 테스트, 문제 진단 등과 같은 활동을 위해 이러한 추적을 재생할 수 있습니다.|[SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|CDC(변경 데이터 캡처) 및 변경 추적 기능에 대해 설명하고 이러한 기능을 사용하여 데이터베이스의 데이터 변경 사항을 추적하는 방법에 대해 설명합니다.|[데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|로그 파일 뷰어를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업 기록, SQL Server 로그, Windows 이벤트 로그 등과 같은 다양한 로그에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 및 메시지를 찾아서 보는 방법에 대해 설명합니다.|[로그 파일 뷰어](../../relational-databases/logs/log-file-viewer.md)|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자를 사용하여 데이터베이스를 분석하고 잠재적 성능 문제를 해결하기 위한 권장 구성을 만드는 방법에 대해 설명합니다.|[데이터베이스 엔진 튜닝 관리자](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|표준 연결이 불가능할 때 프로덕션 데이터베이스 관리자가 인스턴스에 대한 진단 연결을 설정하는 방법에 대해 설명합니다.|[데이터베이스 관리자를 위한 진단 연결](diagnostic-connection-for-database-administrators.md)|  
|사용되지 않는 원격 서버 기능을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 한 인스턴스에서 다른 인스턴스로 액세스하는 방법에 대해 설명합니다. 이 기능에 대한 기본 메커니즘은 연결된 서버입니다.|[원격 서버](remote-servers.md)|  
|메시징 및 큐 애플리케이션에 대한 Service Broker의 기능에 대해 설명하고 Service Broker 설명서에 대한 포인터를 제공합니다.|[Service Broker](sql-server-service-broker.md)|  
|버퍼 풀 확장을 사용하여 I/O 처리량을 크게 향상하기 위해 비휘발성 임의 액세스 스토리지(솔리드 스테이트 드라이브)를 데이터베이스 엔진 버퍼 풀에 빈틈없이 통합하는 방법을 설명합니다.|[버퍼 풀 확장 파일](buffer-pool-extension.md)|  
  
## <a name="see-also"></a>관련 항목  
 [sqlservr 응용 프로그램](../../tools/sqlservr-application.md)   
 [데이터베이스 기능](../../relational-databases/database-features.md)   
 [데이터베이스 엔진 인스턴스 간 기능](../database-engine-cross-instance-features.md)  
  
  
