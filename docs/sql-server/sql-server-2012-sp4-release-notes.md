---
title: "SQL Server 2012 SP4 릴리스 정보 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: 0
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 1d637aa3e820f1acd6dc283030d2cdfa1e6ca074
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-2012-sp4-release-notes"></a>SQL Server 2012 SP4 릴리스 정보
이 항목에서는 SQL Server 2012 SP4에 포함된 향상된 기능을 요약합니다. 또한 SP4를 설치하고 설치 문제를 해결하기 전에 검토해야 하는 문제를 설명합니다. 릴리스 정보는 설치 미디어가 아닌 온라인으로만 제공됩니다. 이 항목은 문제가 발견될 때마다 정기적으로 업데이트됩니다. SP4에 대한 수정 사항의 자세한 목록은 [SQL Server 2012 SP4 릴리스](https://go.microsoft.com/fwlink/?linkid=846937)를 참조하세요.  

> 서비스 팩 4는 모든 SQL Server 2012 SP3 누적 업데이트를 포함합니다.
  
##<a name="download-pages"></a>다운로드 페이지
다음 항목은 SQL Server 2012 SP3의 주 다운로드 패키지에 대한 링크입니다. 다운로드 페이지에 시스템 요구 사항 및 기본 설치 지침이 나와 있습니다.
- [SQL Server 2012 SP4 패치 설치](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)
- [Microsoft SQL Server 2012 SP4 기능 팩](https://go.microsoft.com/fwlink/?linkid=846907)

##  <a name="sp4-performance-and-scale-improvements"></a>SP4 향상된 성능 및 크기 조정 기능

- **향상된 배포 에이전트 정리 프로시저** - 너무 큰 배포 데이터베이스는 차단 및 교착 상태 상황을 발생시켰습니다. 향상된 정리 프로시저는 이러한 일부 차단 또는 교착 상태 시나리오를 제거하려고 합니다. 
- **동적 메모리 개체 크기 조정** - 노드 및 코어 수에 따라 메모리 개체를 동적으로 분할하여 최신 하드웨어의 크기를 조정합니다. 동적 승격을 통해 잠재적인 병목 상태를 방지하고 스레드로부터 안전한 메모리 개체를 자동으로 분할합니다. 분할되지 않은 메모리 개체를 동적으로 승격하여 노드별로 분할할 수 있습니다. 파티션 수는 NUMA 노드 수와 같습니다. 노드별로 분할된 메모리 개체를 다시 승격하여 CPU별로 분할할 수 있습니다. 이 때 파티션 수는 CPU 수와 같습니다.
- **버퍼 풀에 >8TB 사용** - 버퍼 풀 사용량에 128TB 가상 주소 공간을 사용하도록 설정합니다.
- **변경 내용 추적 정리** - 변경 내용 추적 정리 성능 및 변경 내용 추적 쪽 테이블에 대한 효율성을 개선했습니다. 

## <a name="sp4-supportability-and-diagnostics-improvements"></a>SP4 지원 가능성 및 진단 향상

- **복제 에이전트에 대한 전체 덤프 지원** - 현재 복제 에이전트에서 처리되지 않은 예외가 발생하는 경우 기본 동작은 예외 증상의 미니 덤프를 만드는 것입니다. 기본 동작은 처리되지 않은 예외와 깊이 관련된 복잡한 문제를 해결해야 합니다. SP4에서는 복제 에이전트에 대한 전체 덤프 만들기를 지원하는 새 레지스트리 키를 소개합니다.
- **XML 실행 계획에서 향상된 진단** - XML 실행 계획은 사용된 추적 플래그, 중첩된 루프 조인을 최적화하는메모리 조각, CPU 시간 및 경과된 시간에 대한 정보를 노출하도록 향상되었습니다. 
- **진단 XE와 DMV 간의 향상된 상관 관계** - Query_hash 및 query_plan_hash 필드는 쿼리를 고유하게 식별하는 데 사용됩니다. DMV에서는 이를 varbinary(8)으로 정의하는 반면 XEvent에서는 UINT64로 정의합니다. SQL server에 "서명되지 않은 bigint"가 없으므로 캐스팅이 항상 작동하지는 않습니다. 이러한 향상 기능은 query_hash와 query_plan_hash에 해당하는 새 XEvent 작업/필터 열을 소개합니다. 단, XE와 DMV 간에 쿼리의 상관 관계를 지정할 수 있는 INT64로 정의된 경우는 제외합니다. 
- **향상된 메모리 부여/사용량 진단** - 새 query_memory_grant_usage XEvent입니다(Server 2016 SP1의 backport).
- **SSL 협상 단계에 프로토콜 추적 추가** - 성공/실패 협상에 프로토콜 등을 포함한 비트 추적 정보를 추가합니다. 예를 들어, TLS 1.2를 배포하는 동안 연결 시나리오 문제를 해결할 때 유용할 수 있습니다.
- **배포 데이터베이스에 대한 올바른 호환성 수준 설정** - 서비스 팩 설치 후에 배포 데이터베이스 호환성 수준이 90으로 변경됩니다. 이러한 수준은 sp_vupgrade_replication 저장 프로시저에 문제가 발생했기 때문에 변경되었습니다. 이제 배포 데이터베이스에 올바른 호환성 수준을 설정하도록 SP가 변경되었습니다. 
- **데이터베이스 복제를 위한 새 DBCC 명령** - 복제 데이터베이스는 새롭게 추가된 DBCC 명령이며 이를 통해 CSS와 같은 고급 사용자가 데이터 없이 스키마 및 메타데이터를 복제하여 기존 프로덕션 데이터베이스의 문제를 해결할 수 있습니다. 호출은 DBCC clonedatabase에서 수행됩니다('source_database_name', 'clone_database_name'). 복제된 데이터베이스는 프로덕션 환경에서 사용할 수 없습니다. 다음 명령을 사용할 수 있는 복제 데이터베이스에 대한 호출로부터 데이터베이스가 생성되었는지 확인하려면 DATABASEPROPERTYEX('clonedb', 'isClone')를 선택합니다. 1의 반환 값은 true이고 0은 false입니다. 
- **SQL 오류 로그의 TempDB 파일 및 파일 크기 정보** - 시작하는 동안 TempDB 데이터 파일에 대한 크기 및 자동 증가가 다른 경우 파일 수를 인쇄하고 경고를 트리거합니다.
- **SQL Server 오류 로그의 IFI 지원 메시지** - 데이터베이스 인스턴트 파일 초기화를 사용/사용하지 않는 오류 로그에서 표시됩니다.
- **DBCC INPUTBUFFER를 바꾸는 새 DMF** - session_id를 매개 변수로 사용하는 새로운 동적 관리 함수 sys.dm_input_buffer를 도입하여 DBCC INPUTBUFFER를 바꿉니다.
- **가용성 그룹의 읽기 라우팅 실패에 대한 XEvent 향상 기능** - 현재 라우팅 목록이 있지만 해당 목록의 서버가 연결에 사용할 수 없는 경우 read_only_rout_fail XEvent만이 실행됩니다. 이러한 향상 기능은 문제 해결을 지원하기 위한 추가 정보를 포함하고 XEvent를 실행하는 코드 포인트를 확장합니다. 
- **가용성 그룹 장애 조치된 Service Broker의 향상된 처리** - 현재 가용성 그룹 데이터베이스에서 Service Broker를 사용할 때 AG 장애 조치 중에 주 복제본에서 시작된 모든 Service broker 연결이 열려 있게 됩니다. 향상 기능은 AG 장애 조치 중에 이러한 열려 있는 모든 연결을 닫습니다.
- **[자동 소프트 NUMA 분할](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx)**  – SQL 2014 SP2에서 추적 플래그 8079를 서버 수준에서 사용할 때 자동 소프트 NUMA가 도입됩니다. 시작하는 동안 추적 플래그 8079를 사용하면 SQL Server 2014 SP2는 하드웨어 레이아웃에 대해 검사하고 시스템 보고에서 NUMA 노드당 8개 이상의 CPU를 가진 소프트 NUMA를 자동으로 구성합니다. 자동 소프트 NUMA 동작은 하이퍼스레드(HT/논리 프로세서)를 인식합니다. 추가 노드를 분할하고 생성하면 수신기 수, 크기 조정 및 네트워크와 암호화 기능을 늘려서 후순위 처리를 조정합니다. 프로덕션 환경에서 설정하기 전에 자동 소프트 NUMA를 사용하여 워크로드의 성능을 첫 번째로 테스트하는 것이 좋습니다.

## <a name="see-also"></a>관련 항목:
- [SQL Server 2012 서비스 업데이트 설치](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [SQL Server 버전 및 에디션 확인 방법](https://support.microsoft.com/en-us/help/321185)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
