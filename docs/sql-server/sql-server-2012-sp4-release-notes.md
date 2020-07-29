---
title: SQL Server 2012 서비스 팩 릴리스 정보 | Microsoft Docs
description: 이 문서는 네 가지 SQL Server 2012 서비스 팩의 통합 릴리스 정보를 포함합니다. 각 서비스 팩은 이전 서비스 팩에 누적됩니다.
ms.prod: sql
ms.technology: release-landing
ms.custom: ''
ms.date: 07/22/2020
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
author: rothja
ms.author: jroth
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 395acfc882bdd4277a260f53eba4da8acf57d85f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111690"
---
# <a name="sql-server-2012-service-pack-release-notes"></a>SQL Server 2012 서비스 팩 릴리스 정보
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]
이 토픽은 네 가지 SQL Server 2012 서비스 팩의 통합 릴리스 정보를 포함합니다. 각 서비스 팩은 이전 서비스 팩에 누적됩니다.

서비스 팩은 설치 미디어로 제공되지 않고 온라인으로만 사용할 수 있으며 다음과 같이 다운로드할 수 있습니다.
- [SQL Server 2012 SP4](https://go.microsoft.com/fwlink/?linkid=846937)
- [SQL Server 2012 SP3](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)
- [SQL Server 2012 SP2](https://support.microsoft.com/KB/2958429)
- [SQL Server 2012 SP1](https://go.microsoft.com/fwlink/p/?LinkID=268158)

## <a name="service-pack-4-release-notes"></a>서비스 팩 4 릴리스 정보

### <a name="download-pages"></a>다운로드 페이지

- [SQL Server 2012 SP4 기능 팩](https://www.microsoft.com/download/details.aspx?id=56041)
- [SQL Server 2012 SP4 패치 설치](https://www.microsoft.com/download/details.aspx?id=56040)
- [SQL Server 2012 SP4 Express](https://www.microsoft.com/download/details.aspx?id=56042)


### <a name="performance-and-scale-improvements"></a>향상된 성능 및 크기 조정 기능
- **향상된 배포 에이전트 정리 프로시저** - 너무 큰 배포 데이터베이스는 차단 및 교착 상태 상황을 발생시켰습니다. 향상된 정리 프로시저는 이러한 일부 차단 또는 교착 상태 시나리오를 제거하려고 합니다. 
- **동적 메모리 개체 크기 조정** - 노드 및 코어 수에 따라 메모리 개체를 동적으로 분할하여 최신 하드웨어의 크기를 조정합니다. 동적 승격을 통해 잠재적인 병목 상태를 방지하고 스레드로부터 안전한 메모리 개체를 자동으로 분할합니다. 분할되지 않은 메모리 개체를 동적으로 승격하여 노드별로 분할할 수 있습니다. 파티션 수는 NUMA 노드 수와 같습니다. 노드별로 분할된 메모리 개체를 다시 승격하여 CPU별로 분할할 수 있습니다. 이 때 파티션 수는 CPU 수와 같습니다.
- **버퍼 풀에 >8TB 사용** - 버퍼 풀 사용량에 128TB 가상 주소 공간을 사용하도록 설정합니다.
- **변경 내용 추적 정리** - 변경 내용 추적 정리 성능 및 변경 내용 추적 쪽 테이블에 대한 효율성을 개선했습니다. 

### <a name="supportability-and-diagnostics-improvements"></a>지원 가능성 및 진단 향상
- **복제 에이전트에 대한 전체 덤프 지원** - 현재 복제 에이전트에서 처리되지 않은 예외가 발생하는 경우 기본 동작은 예외 증상의 미니 덤프를 만드는 것입니다. 기본 동작은 처리되지 않은 예외와 깊이 관련된 복잡한 문제를 해결해야 합니다. SP4에서는 복제 에이전트에 대한 전체 덤프 만들기를 지원하는 새 레지스트리 키를 소개합니다.
- **XML 실행 계획에서 향상된 진단** - XML 실행 계획은 사용된 추적 플래그, 중첩된 루프 조인을 최적화하는메모리 조각, CPU 시간 및 경과된 시간에 대한 정보를 노출하도록 향상되었습니다. 
- **진단 XE와 DMV 간의 향상된 상관 관계** - Query_hash 및 query_plan_hash 필드는 쿼리를 고유하게 식별하는 데 사용됩니다. DMV에서는 이를 varbinary(8)으로 정의하는 반면 XEvent에서는 UINT64로 정의합니다. SQL 서버에 "서명되지 않은 bigint"가 없으므로 캐스팅이 항상 작동하지는 않습니다. 이러한 향상 기능은 query_hash와 query_plan_hash에 해당하는 새 XEvent 작업/필터 열을 소개합니다. 단, XE와 DMV 간에 쿼리의 상관 관계를 지정할 수 있는 INT64로 정의된 경우는 제외합니다. 
- **향상된 메모리 부여/사용량 진단** - 새 query_memory_grant_usage XEvent입니다(Server 2016 SP1의 backport).
- **SSL 협상 단계에 프로토콜 추적 추가** - 성공/실패 협상에 프로토콜 등을 포함한 비트 추적 정보를 추가합니다. 예를 들어, TLS 1.2를 배포하는 동안 연결 시나리오 문제를 해결할 때 유용할 수 있습니다.
- **배포 데이터베이스에 대한 올바른 호환성 수준 설정** - 서비스 팩 설치 후에 배포 데이터베이스 호환성 수준이 90으로 변경됩니다. 이러한 수준은 sp_vupgrade_replication 저장 프로시저에 문제가 발생했기 때문에 변경되었습니다. 이제 배포 데이터베이스에 올바른 호환성 수준을 설정하도록 SP가 변경되었습니다. 
- **데이터베이스 복제를 위한 새 DBCC 명령** - 복제 데이터베이스는 새롭게 추가된 DBCC 명령이며 이를 통해 CSS와 같은 고급 사용자가 데이터 없이 스키마 및 메타데이터를 복제하여 기존 프로덕션 데이터베이스의 문제를 해결할 수 있습니다. 호출은 DBCC clonedatabase에서 수행됩니다('source_database_name', 'clone_database_name'). 복제된 데이터베이스는 프로덕션 환경에서 사용할 수 없습니다. 다음 명령을 사용할 수 있는 복제 데이터베이스에 대한 호출로부터 데이터베이스가 생성되었는지 확인하려면 DATABASEPROPERTYEX('clonedb', 'isClone')를 선택합니다. 1의 반환 값은 true이고 0은 false입니다. 
- **SQL 오류 로그의 TempDB 파일 및 파일 크기 정보** - 시작하는 동안 TempDB 데이터 파일에 대한 크기 및 자동 증가가 다른 경우 파일 수를 인쇄하고 경고를 트리거합니다.
- **SQL Server 오류 로그의 IFI 지원 메시지** - 데이터베이스 인스턴트 파일 초기화를 사용/사용하지 않는 오류 로그에서 표시됩니다.
- **DBCC INPUTBUFFER를 바꾸는 새 DMF** - session_id를 매개 변수로 사용하는 새로운 동적 관리 함수 sys.dm_input_buffer를 도입하여 DBCC INPUTBUFFER를 바꿉니다.
- **가용성 그룹의 읽기 라우팅 실패에 대한 XEvent 향상 기능** - 현재 라우팅 목록이 있지만 해당 목록의 서버가 연결에 사용할 수 없는 경우 read_only_rout_fail XEvent만이 실행됩니다. 이러한 향상 기능은 문제 해결을 지원하기 위한 추가 정보를 포함하고 XEvent를 실행하는 코드 포인트를 확장합니다. 
- **가용성 그룹 장애 조치된 Service Broker의 향상된 처리** - 현재 가용성 그룹 데이터베이스에서 Service Broker를 사용할 때 AG 장애 조치 중에 주 복제본에서 시작된 모든 Service broker 연결이 열려 있게 됩니다. 향상 기능은 AG 장애 조치 중에 이러한 열려 있는 모든 연결을 닫습니다.
- **자동 Soft-NUMA 분할** – SQL 2014 SP2에서 추적 플래그 8079를 서버 수준에서 사용할 때 자동 [Soft-NUMA](../database-engine/configure-windows/soft-numa-sql-server.md) 분할이 도입됩니다. 시작하는 동안 추적 플래그 8079를 사용하면 SQL Server 2014 SP2는 하드웨어 레이아웃에 대해 검사하고 시스템 보고에서 NUMA 노드당 8개 이상의 CPU를 가진 소프트 NUMA를 자동으로 구성합니다. 자동 소프트 NUMA 동작은 하이퍼스레드(HT/논리 프로세서)를 인식합니다. 추가 노드를 분할하고 생성하면 수신기 수, 크기 조정 및 네트워크와 암호화 기능을 늘려서 후순위 처리를 조정합니다. 프로덕션 환경에서 설정하기 전에 자동 소프트 NUMA를 사용하여 워크로드의 성능을 첫 번째로 테스트하는 것이 좋습니다.

## <a name="service-pack-3-release-notes"></a>서비스 팩 3 릴리스 정보

### <a name="download-pages"></a>다운로드 페이지
- [SQL Server 2012 SP3 기능 팩](https://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](https://go.microsoft.com/fwlink/?linkid=692144)

현재 설치된 버전에 따라 다운로드할 파일의 이름과 위치를 확인하기 위한 자세한 내용은 [SQL Server 2012 Service Pack 3 release information](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)(SQL Server 2012 서비스 팩 3 릴리스 정보)에서 “Select the correct file to download”(다운로드할 올바른 파일 선택) 섹션을 참조하세요.

## <a name="service-pack-2-release-notes"></a>서비스 팩 2 릴리스 정보
  
### <a name="download-pages"></a>다운로드 페이지 
- [SQL Server 2012 SP2 기능 팩](https://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](https://go.microsoft.com/fwlink/?LinkID=401007)

아래 표에서 현재 설치된 버전에 따라 다운로드할 파일의 위치와 이름을 확인하세요. 다운로드 페이지에 시스템 요구 사항 및 기본 설치 지침이 나와 있습니다.  

|현재 설치된 버전|원하는 작업|다운로드 및 설치할 파일|  
|---|---|---|   
|32비트 설치:|||  
|32비트 버전의 SQL  Server  2012|32비트 버전의 SQL Server 2012 SP2로 업그레이드|**SQL Server 2012 SP2 다운로드 페이지**<arch> **-** <lang id>**에 있는** SQLServer2012SP2-KB2958429- [.exe](https://go.microsoft.com/fwlink/?LinkID=401006)|  
|32비트 버전의 SQL  Server  2012  RTM  Express|32비트 버전의 SQL Server 2012 Express SP2으로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPR_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|32비트 버전의 SQL  Server  2012  클라이언트 및 관리 도구(SQL  Server  2012  Management  Studio  포함)|32비트 버전의 SQL Server 2012 SP2로 클라이언트 및 관리 도구 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPRWT_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|32비트 버전의 SQL  Server  2012  Management  Studio  Express|32비트 버전의 SQL Server 2012 SP2 Management Studio Express로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLManagementStudio_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|32비트 버전의 SQL Server 2012 및 32비트 버전의 클라이언트 및 관리 도구(SQL Server 2012 RTM Management Studio 포함)|32비트 버전의 SQL Server 2012 SP2로 모든 제품 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPRADV_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM 기능 팩](https://www.microsoft.com/download/details.aspx?id=29065) 또는 [Microsoft SQL Server 2012 SP1 기능 팩](https://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 32비트 버전 도구 하나 이상|32비트 버전의 Microsoft SQL Server 2012 SP2 Feature Pack으로 도구 업그레이드|Microsoft [SQL Server 2012 SP2 기능 팩 다운로드 페이지](https://go.microsoft.com/fwlink/?LinkID=401008)에 있는 도구 하나 이상|  
|64비트 설치:|||  
|64비트 버전의 SQL Server 2012|64비트 버전의 SQL Server 2012 SP2로 업그레이드|<arch>-<langid>SQL Server 2012 SP2 다운로드 페이지 [에 있는 SQLServer2012SP2-KB2958429-](https://go.microsoft.com/fwlink/?LinkID=401006).exe|  
|64비트 버전의 SQL Server 2012 RTM Express|64비트 버전의 SQL Server 2012 SP2로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPR_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|64비트 버전의 SQL Server 2012 클라이언트 및 관리 효율성 도구(SQL Server 2012 Management Studio 포함)|64비트 버전의 SQL Server 2012 SP2로 클라이언트 및 관리 효율성 도구 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLEXPRWT_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|64비트 버전의 SQL Server 2012 Management Studio Express|64비트 버전의 SQL Server 2012 SP2 Management Studio Express로 업그레이드|**SQL Server 2012 SP2 Express 다운로드 페이지**<arch>**에 있는**<lang>**SQLManagementStudio_** _ [.msi](https://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM 기능 팩](https://www.microsoft.com/download/details.aspx?id=29065) 또는 [Microsoft SQL Server 2012 SP1 기능 팩](https://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 64비트 버전 도구 하나 이상|64비트 버전의 Microsoft SQL Server 2012 SP2 Feature Pack으로 도구 업그레이드|Microsoft [SQL Server 2012 SP2 기능 팩 다운로드 페이지](https://go.microsoft.com/fwlink/?LinkID=401008)에 있는 도구 하나 이상|   


## <a name="service-pack-1-release-notes"></a>서비스 팩 1 릴리스 정보

### <a name="download-pages"></a>다운로드 페이지  
- [SQL Server 2012 SP1 기능 팩](https://go.microsoft.com/fwlink/p/?LinkID=268158)
- [SQL Server 2012 SP1 Express](https://www.microsoft.com/download/details.aspx?id=35579)


다음 표를 사용하여 다운로드 및 설치할 파일을 결정합니다. 서비스 팩을 설치하기 전에 올바른 시스템 요구 사항을 갖추고 있는지 확인합니다. 시스템 요구 사항은 표에 링크되어 있는 다운로드 페이지에서 확인할 수 있습니다.  

|현재 설치된 버전|원하는 작업|다운로드 및 설치할 파일|  
|---|---|---|  
|**32비트 설치:**|||  
|32비트 버전의 SQL  Server  2012|32비트 버전의 SQL  Server  2012  SP1로 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x86-ENU.exe|  
|32비트 버전의 SQL  Server  2012  RTM  Express|32비트 버전의 SQL  Server  2012  Express  SP1으로 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x86-ENU.exe|  
|32비트 버전의 SQL  Server  2012  클라이언트 및 관리 도구(SQL  Server  2012  Management  Studio  포함)|32비트 버전의 SQL  Server  2012  SP1로 클라이언트 및 관리 도구 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전의 SQL  Server  2012  Management  Studio  Express|32비트 버전의 SQL  Server  2012  SP1  Management  Studio  Express로 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전의 SQL Server 2012 **및** 32비트 버전의 클라이언트 및 관리 도구(SQL Server 2012 RTM Management Studio 포함)|32비트 버전의 SQL  Server  2012  SP1로 모든 제품 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x86-ENU.exe|  
|32비트 버전의 [Microsoft SQL Server 2012 RTM 기능 팩](https://www.microsoft.com/download/details.aspx?id=44272)에 있는 도구 하나 이상|32비트 버전의 Microsoft  SQL  Server  2012  SP1  기능 팩으로 도구 업그레이드|[Microsoft  SQL  Server  2012  SP1  기능 팩](https://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 파일 하나 이상|  
|SQL  Server  2012의 32비트 설치 없음|32비트 Server  2012(SP1  포함)  설치(SP1이 미리 설치된 새 인스턴스)|**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x86-ENU.exe [및](https://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x86-ENU.box|  
|SQL  Server  2012  Management  Studio의 32비트 설치 없음|32비트 SQL  Server  2012  Management  Studio(SP1포함)  설치|[여기](https://go.microsoft.com/fwlink/p/?LinkId=267905)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전의 SQL  Server  2012  RTM  Express  없음|32비트 SQL  Server  2012  Express(SP1포함)  설치|[여기](https://go.microsoft.com/fwlink/p/?LinkId=267905)에 있는 SQLEXPR32_x86_ENU.exe|  
|**SQL Server 2008** 또는 **SQL Server 2008 R2**의 32비트 설치|32비트 SQL Server 2012(SP1 포함)로**전체 업그레이드**|**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x86-ENU.exe [및](https://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x86-ENU.box|  
|**64비트 설치:**|||  
|64비트 버전의 SQL Server 2012|64비트 버전의 SQL Server 2012 SP1로 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x64-ENU.exe|  
|64비트 버전의 SQL Server 2012 RTM Express|64비트 버전의 SQL Server 2012 SP1로 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x64-ENU.exe|  
|64비트 버전의 SQL Server 2012 클라이언트 및 관리 효율성 도구(SQL Server 2012 Management Studio 포함)|64비트 버전의 SQL Server 2012 SP1로 클라이언트 및 관리 효율성 도구 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전의 SQL Server 2012 Management Studio Express|64비트 버전의 SQL Server 2012 SP1 Management Studio Express로 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전의 SQL Server 2012 **및** 64비트 버전의 클라이언트 및 관리 도구(SQL Server 2012 RTM Management Studio 포함)|64비트 버전의 SQL Server 2012 SP1로 모든 제품 업그레이드|[여기](https://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x64-ENU.exe|  
|64비트 버전의 [Microsoft SQL Server 2012 RTM 기능 팩](https://www.microsoft.com/download/details.aspx?id=44272)에 있는 도구 하나 이상|64비트 버전의 Microsoft SQL Server 2012 SP1 Feature Pack으로 도구 업그레이드|[Microsoft  SQL  Server  2012  SP1  기능 팩](https://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 파일 하나 이상|  
|SQL Server 2012의 64비트 설치 없음|64비트 Server 2012(SP1 포함) 설치(SP1이 미리 설치된 새 인스턴스)|**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x64-ENU.exe [및](https://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x64-ENU.box|  
|SQL Server 2012 Management Studio의 64비트 설치 없음|64비트 SQL Server 2012 Management Studio(SP1 포함) 설치|[여기](https://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전의 SQL Server 2012 RTM  Express 없음|64비트 SQL Server 2012 Express(SP1포함) 설치|[여기](https://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLEXPR_x64_ENU.exe|  
|**SQL Server 2008** 또는 **SQL Server 2008 R2**64비트 설치|64비트 SQL Server 2012(SP1 포함)로**전체 업그레이드**|**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x64-ENU.exe [및](https://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x64-ENU.box|  

### <a name="known-issues-fixed-in-this-service-pack"></a>이 서비스 팩에서 해결된 알려진 문제  
이 서비스 팩에서 해결된 전체 버그 및 알려진 문제 목록은 [이 KB 문서](https://support.microsoft.com/kb/2674319)를 참조하세요.   

### <a name="reinstalling--instances-of-sql-server-failover-cluster-fails-if-you-use-the-same-ip-address"></a>동일한 IP 주소를 사용하는 경우 SQL Server 장애 조치(Failover) 클러스터 인스턴스의 다시 설치가 실패함  
**문제:** SQL Server 장애 조치(Failover) 클러스터 인스턴스를 설치하는 동안 잘못된 IP 주소를 지정하는 경우 설치에 실패합니다. 실패한 인스턴스를 제거한 후 올바른 IP 주소와 동일한 인스턴스 이름을 사용하여 SQL Server 장애 조치(Failover) 클러스터 인스턴스를 다시 설치하려고 하면 설치에 실패합니다. 이 오류는 이전 설치로 인해 중복된 리소스 그룹이 남겨졌기 때문에 발생합니다.  
  
**해결 방법:** 이 문제를 해결하려면 설치하는 동안 다른 인스턴스 이름을 사용하거나 다시 설치하기 전에 리소스 그룹을 수동으로 삭제하세요. 자세한 내용은 [SQL  Server  장애 조치(failover)  클러스터에서 노드 추가 또는 제거](failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하십시오. 
  
### <a name="analysis-services-and-powerpivot"></a>Analysis Services 및 PowerPivot  
  
##### <a name="powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>PowerPivot 구성 도구로 PowerPivot 갤러리가 만들어지지 않음  
**문제:** PowerPivot 구성 도구는 팀 사이트를 프로비저닝하므로 PowerPivot 갤러리가 만들어지지 않습니다.  
  
**해결 방법:** 새 앱(라이브러리)을 만듭니다.  
  
1.  사이트 모음 기능 **사이트 모음에 대한 PowerPivot  기능 통합** 이 활성 상태인지 확인합니다.  
  
2.  기존 사이트의 **사이트 콘텐츠** 페이지에서 **앱 추가**를 클릭합니다.  
  
3.  **PowerPivot  갤러리**를 클릭합니다.  
  
#### <a name="to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>Excel 2013에서 PowerPivot for Excel을 사용하려면 Excel과 함께 설치된 추가 기능을 사용해야 합니다.  
**문제:** Office 2010을 사용하는 경우 PowerPivot for Excel은 독립 실행형 추가 기능으로, [https://www.microsoft.com/bi/powerpivot.aspx](https://www.microsoft.com/bi/powerpivot.aspx)에서 다운로드할 수 있습니다. 또는 [Microsoft  다운로드 센터](https://www.microsoft.com/download/details.aspx?id=29074)에서 다운로드할 수도 있습니다. 다운로드로 제공되는 두 가지 버전의 PowerPivot 추가 기능이 있습니다. 하나는 SQL Server 2008 R2와 함께 제공되는 버전이고, 다른 하나는 SQL Server 2012와 함께 제공되는 버전입니다. 그러나 Office 2013의 경우 PowerPivot for Excel은 Office와 함께 제공되며 Excel과 함께 설치됩니다. SQL Server 2008 R2 및 SQL Server 2012 버전의 PowerPivot for Excel 2010이 Excel 2013과 호환되지 않지만 Excel 2010을 Excel 2013과 함께 실행하려면 PowerPivot for Excel 2010을 클라이언트 컴퓨터에 설치할 수 있습니다. 즉, 두 버전의 Excel이 공존할 수 있으므로 해당 PowerPivot 추가 기능을 사용할 수 있습니다.  
  
**해결 방법:** PowerPivot for Excel 2013을 사용하려면 COM 추가 기능을 사용해야 합니다. Excel 2013에서 **파일** | **옵션** | **추가 기능**을 선택합니다. **관리** 드롭다운 상자에서 **COM 추가 기능** 을 선택하고 **이동**을 클릭합니다. **COM 추가 기능**에서 **Microsoft Office PowerPivot for Excel 2013** 을 선택하고 **확인**을 클릭합니다.  
  
### <a name="reporting-services"></a>Reporting Services  
  
#### <a name="install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>Reporting Services를 설치하기 전에 SharePoint Server 2013 설치 및 구성  
**문제:** SSRS(SQL Server Reporting Services)를 설치하기 **전**에 다음 요구 사항을 완료해야 합니다.  
  
1.  SharePoint  2013  제품 준비 도구를 실행합니다.  
  
2.  SharePoint  Server  2013을 설치합니다.  
  
3.  SharePoint  2013  제품 구성 마법사를 실행하거나 해당 구성 단계를 완료하여 SharePoint  팜을 구성합니다.  
  
**해결 방법:**  SharePoint 팜을 구성하기 전에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드를 설치한 경우 필요한 해결 방법은 설치된 다른 구성 요소에 따라 다릅니다.  
  
#### <a name="power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>SharePoint Server 2013의 Power View에 Microsoft.AnalysisServices.SPClient.dll이 필요함  
**문제:** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 필수 구성 요소인 **Microsoft.AnalysisServices.SPClient.dll**을 설치하지 않습니다. SharePoint 모드에서 SharePoint Server 2013 미리 보기 및 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 를 설치하지만 SharePoint 2013용 PowerPivot 설치 관리자 패키지인 **spPowerPivot.msi** 를 다운로드 및 설치하지 않는 경우, 파워 뷰가 작동하지 않고 파워 뷰에서 다음 증상이 나타납니다.  
  
**증상:** 파워 뷰 보고서를 만들려고 하면 다음과 비슷한 오류 메시지가 표시됩니다.  
  
-   "데이터 원본에 대한 연결을 설정할 수 없습니다..."  
  
내부 오류 세부 정보에는 다음과 비슷한 메시지가 포함됩니다.  
  
-   연결 문자열 속성 '사용자 ID'에 값 'SharePoint  Principal'이 지원되지 않습니다."  
  
**해결 방법:** SharePoint Server 2013에서 SharePoint 2013용 PowerPivot 설치 관리자 패키지(**spPowerPivot.msi**)를 설치합니다. 설치 관리자 패키지는 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 기능 팩의 일부로 사용할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 다운로드 센터의 [SQL  Server  2012  SP1  기능 팩](https://go.microsoft.com/fwlink/p/?LinkID=268266)에서 기능 팩을 다운로드할 수 있습니다.  
  
#### <a name="power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>예약된 데이터 새로 고침 후 PowerPivot 통합 문서의 파워 뷰 시트가 삭제됨  
**문제**: SharePoint용 PowerPivot 추가 기능에서 파워 뷰가 있는 통합 문서에 **예약된 데이터 새로 고침**을 사용하면 파워 뷰 시트가 모두 삭제됩니다.  
  
**해결 방법**: 파워 뷰 통합 문서에 **예약된 데이터 새로 고침**을 사용하려면 데이터 모델인 PowerPivot 통합 문서를 만듭니다. 데이터 모델이 있는 PowerPivot  통합 문서에 연결되는 Power  View  시트 및 Excel  시트로 별도의 통합 문서를 만듭니다. 데이터 모델이 있는 PowerPivot  통합 문서에 대해서만 데이터 새로 고침 예약을 수행해야 합니다.  
  
### <a name="data-quality-services"></a>데이터베이스 엔진 서비스  
  
#### <a name="dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>DQS를 잘못된 버전의 SQL Server 2012에서 사용할 수 있음  
**문제:** [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM 릴리스에서 DQS(Data Quality Services) 기능은 Enterprise, Business Intelligence 및 Developer 버전 이외의 SQL Server 버전에서 사용할 수 있습니다. SQL  Server  2012  SP1을 설치하면 DQS는 Enterprise,  Business  Intelligence  및 Developer  버전을 제외한 모든 버전에서 사용할 수 있습니다.  
  
**해결 방법**: 지원되지 않는 버전에서 DQS를 사용하는 경우에는 지원되는 버전으로 업그레이드하거나 애플리케이션에서 이 기능에 대한 종속성을 제거합니다.  
  
### <a name="sql-server-express"></a>SQL Server Express  
  
#### <a name="full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>SQL Server 2012 Express SP1에서 사용할 수 있는 SQL Server Management Studio의 전체 버전  
SQL  Server  2012  Express  서비스 팩 1(SP1)  릴리스에는 SQL  Server  2012  Management  Studio  Express  대신 SQL  Server  2012  Management  Studio의 전체 버전(이전에는 SQL  Server  2012  DVD에서만 사용 가능)이 포함되어 있습니다. SQL  Server  2012  Express  SP1을 다운로드하고 설치하려면 [SQL  Server  2012  Express  서비스 팩 1](https://go.microsoft.com/fwlink/p/?linkid=267905)을 참조하십시오.  
  
### <a name="change-data-capture-service-and-designer-for-oracle-by-attunity"></a>Change Data Capture Service 및 Designer for Oracle by Attunity  
  
#### <a name="upgrading-the-cdc-service-and-designer"></a>CDC Service 및 Designer 업그레이드  
**문제:** SQL Server 2012 SP1 설치 시 Change Data Capture Designer for Oracle 및 Change Data Capture Service for Oracle by Attunity가 머신에 설치되는 경우 SP1을 설치해도 이러한 구성 요소가 업그레이드되지 않습니다.  
  
**해결 방법:** CDC 구성 요소를 최신 버전으로 업그레이드하려면 다음을 수행합니다.  
  
1.  [SQL  Server  2012  SP1  기능 팩 다운로드 페이지](https://go.microsoft.com/fwlink/p/?LinkID=268266)에서 Change  Data  Capture  Service  for  Oracle  by  Attunity의 .msi  파일을 다운로드합니다.  
  
2.  .msi  파일을 실행합니다.  
  
### <a name="sql-server-data-tier-application-framework-dacfx"></a>DACFx(SQL Server Data-Tier Application Framework)  
**현재 위치 업그레이드 지원**  
  
이 버전의 데이터 계층 애플리케이션 프레임워크(DACFx)에서는 이전 버전에서의 내부 업그레이드를 지원하므로 이 릴리스로 업그레이드하기 전에 이전 DACFx 설치를 제거할 필요가 없습니다. [여기](https://msdn.microsoft.com/library/dn702988.aspx)에서 DACFx  후속 릴리스를 찾을 수 있습니다.  
  
**선택적 XML 인덱스 지원**  
  
SQL Server 2012 SP1에는 높아진 성능과 효율성으로 XML 열 데이터를 인덱싱하는 새로운 방법을 제공하는 새로운 SQL Server 기능인 [SXI(선택적 XML 인덱스)](https://msdn.microsoft.com/598ecdcd-084b-4032-81b2-eed6ae9f5d44)에 대한 지원이 포함되어 있습니다.  
  
이제 DACFx에서는 모든 DAC  시나리오 및 클라이언트 도구에서의 SXI  인덱스를 지원합니다. SXI는 최신 버전의 SSDT에서만 지원됩니다. SSDT  RTM  및 2012년 9월 버전에서는 SXI를 지원하지 않습니다.  
  
**네이티브 BCP 데이터 형식 지원**  
  
이전에는 DACPAC  및 BACPAC  패키지 내부에 테이블 데이터를 저장하는 데 JSON  데이터 형식을 사용했습니다. 이 업데이트를 통해 이제 네이티브 BCP가 데이터 지속성 형식입니다. 이러한 변경으로 SQL_Variant  형식에 대한 지원을 비롯하여 DACFx에 대한 SQL  Server  데이터 형식 정확성이 향상되고 대규모 데이터베이스의 데이터 배포 성능이 향상되었습니다.  
  
**패키지 생성/배포 시 CHECK 제약 조건 상태를 보존**  
  
이전에는 DACFx가 데이터베이스 스키마의 테이블에 정의된 CHECK  제약 조건의 상태(WITH  CHECK/NOCHECK)를 보존하지 않았으며 이 정보를 DACPAC  내부에 저장하지 않았습니다. CHECK  제약 조건을 위반하는 기존 테이블 데이터가 있는 경우 이 동작으로 인해 패키지 배포 시 문제가 발생할 수 있었습니다. 이 업데이트를 통해 이제 DACFx는 데이터베이스에서 추출할 때 DACPAC  내에 CHECK  제약 조건의 현재 상태를 저장하고 패키지 배포 시 이 상태를 적절하게 복원합니다.  
  
**SqlPackage.exe(DACFx 명령줄 도구) 업데이트**  
  
-   데이터가 있는 DACPAC 추출 – 데이터베이스 스키마와 함께 사용자 테이블의 데이터를 포함하는 라이브 SQL Server 또는 Azure SQL Database로부터 데이터베이스 스냅샷 파일(.dacpac)을 만듭니다. 이러한 패키지는 SqlPackage.exe 게시 작업을 사용하여 새로운 또는 기존의 SQL Server 또는 Azure SQL Database에 게시할 수 있습니다. 패키지에 포함된 데이터는 대상 데이터베이스의 기존 데이터를 대체합니다.  
  
-   BACPAC 내보내기 - 온-프레미스 SQL Server에서 Azure SQL Database로 데이터베이스를 마이그레이션하는 데 사용할 수 있는 데이터베이스 스키마 및 사용자 데이터를 포함하는 라이브 SQL Server 또는 Azure SQL Database의 논리적 백업 파일(.bacpac)을 만듭니다. Azure와 호환되는 데이터베이스를 내보낸 다음 나중에 지원되는 버전의 SQL  Server 간에 가져올 수 있습니다.  
  
-   BACPAC 가져오기 – .bacpac 파일을 가져와서 새로 만들거나 빈 SQL Server 또는 Azure SQL Database를 채웁니다.  
  
MSDN의 전체 SqlPackage.exe 설명서는 [여기](https://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx)에 있습니다.  
  
**패키지 호환성**  
  
이 릴리스에는 DAC  패키지에 대한 몇 가지 이후 버전과의 호환성 시나리오가 도입되었습니다.  
  
-   이 릴리스에서 만든 DAC  패키지 중 SXI  요소 또는 테이블 데이터가 없는 패키지는 이전 릴리스의 DACFx(SQL Server 2012 RTM, SQL Server 2012 CU1 및 DACFx 2012년 9월 버전)에서 사용될 수 있습니다.  
  
-   이 버전의 DACFx에서 만든 모든 DAC  패키지는 이 릴리스에서 사용될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목
- [SQL Server 2012 서비스 업데이트 설치](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [SQL Server 버전 및 에디션 확인 방법](https://support.microsoft.com/help/321185)
- [SQL Server 2012 서비스 업데이트 설치](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [SQL Server 버전 및 에디션 확인 방법](https://support.microsoft.com/help/321185) 
- [SQL  Server  버전 및 에디션 확인 방법](https://support.microsoft.com/kb/321185)  
- [SQL Server 2014 버전에서 지원하는 기능](https://msdn.microsoft.com/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
