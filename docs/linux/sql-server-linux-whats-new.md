---
title: "Linux에서 SQL Server 2017 r c 1에 대 한 새로운 기능 | Microsoft Docs"
description: "이 항목의 SQL Server 2017 Linux에서 현재 릴리스에 대 한 새로운 강조 표시 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 649c7cbd03b6d2e61dbbb572a34cdbcd2a7ab7cd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>SQL Server 2017 linux에 대 한 새로운 기능

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 SQL Server 2017 Linux에서 실행 중인에 대 한 새로운 설명입니다.

## <a name="rc2"></a>RC2

RC2 릴리스 버그가 수정 및 향상 된 기능을 포함합니다.

## <a name="rc1"></a>RC1

RC1 릴리스는 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- 암호화 된 연결에 대 한 투명 한 계층 TLS (보안)를 사용할 수 있습니다. 자세한 내용은 참조 [Linux에서 SQL Server 연결 암호화](sql-server-linux-encrypted-connections.md)합니다.
- 활성화 [Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.
- 활성화 [DB 메일](../relational-databases/database-mail/database-mail.md)합니다.
- IPV6 지원을 추가 했습니다.
- 초기 SQL Server 설치 프로그램에 대 한 추가 된 환경 변수입니다. 자세한 내용은 참조 [Linux에서 환경 변수를 사용 하 여 SQL Server 구성 설정](sql-server-linux-configure-environment-variables.md)합니다.
- 제거 **sqlpackage** 에서 이진 파일을 설치 합니다. SqlPackage 계속 실행할 수 있습니다 Linux에 대해 원격으로 Windows에서.
- 공유 디스크 클러스터 리소스 에이전트 집합 Windows SQL Server 장애 조치 클러스터 인스턴스에서 같은 리소스 이름입니다. `@@ServerName`SQL Server 공유 디스크 클러스터 리소스 이름; 반환 RC1 이전 리소스를 소유 하는 클러스터 노드의 이름을 반환 합니다.

## <a name="ctp-21"></a>CTP 2.1

CTP 2.1 릴리스에 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- 추가 [SQL Server 서비스를 구성 하려면 환경 변수](sql-server-linux-configure-environment-variables.md)합니다.
- [mssql conf](sql-server-linux-configure-mssql-conf.md) 설정에 대 한 명명 규칙을 두 부분으로 구성 해야 합니다.
- [mssql scripter](https://github.com/Microsoft/sql-xplat-cli) 도구입니다. 이 유틸리티를 생성 개발자, Dba, 및 시스템 관리자를 사용 하면 `CREATE` 및 `INSERT` 명령줄에서 SQL Server, Azure SQL DB 및 Azure SQL DW 데이터베이스의 데이터베이스 개체에서 Transact SQL 스크립트.
- [DBFS 도구](https://github.com/Microsoft/dbfs)합니다. Linux 운영 체제에서 가상 디렉터리의 가상 파일을 Dba와 시스템 관리자는 SQL Server 동적 관리 뷰 (Dmv)에서 라이브 데이터를 노출 하 여 SQL Server를 더욱 쉽게 모니터링할 수 있도록 하는 오픈 소스 도구입니다.
- SQL Server Integration Services (SSIS)는 이제 Linux에서 실행 됩니다. 또한 명령줄에서는 Linux에서 SSIS 패키지를 실행할 수 있는 새 패키지가 있습니다. 자세한 내용은 참조는 [Linux에 대 한 SSIS 지원 블로그 게시물 발표](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)합니다. Linux CTP 2.1 새로 고침에 대 한 SSIS, SSIS 패키지는 Linux 기반 ODBC 연결 사용할 수 있습니다. 자세한 내용은 참조는 [블로그 게시물 Linux ODBC 지원 발표](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

## <a name="ctp-20"></a>CTP 2.0

CTP 2.0 릴리스는 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- 추가 **로그 전달** SQL Server 에이전트에 대 한 기능입니다.
- Mssql 구성의 지역화 된 메시지
- Linux 경로 서식을 전체 SQL Server 엔진에서 호환 됩니다. 에 대 한 지원 하지만 "c:\\" 접두사가 지정 된 경로 계속 됩니다.
- DMV를 사용 하도록 설정 **sys.dm_os_file_exists**합니다.
- DMV를 사용 하도록 설정 **sys.fn_trace_gettable**합니다.
- 추가 [CLR 엄격한 보안 모드](/sql/database-engine/configure-windows/clr-strict-security)합니다.
- SQL 그래프입니다.
- 다시 시작 가능한 온라인 인덱스 다시 작성 합니다.
- 선택 쿼리를 처리 합니다.
- Utf-8 인코딩을 로그 파일 등의 시스템 파일을 추가 합니다.
- 메모리 내 데이터베이스 위치 제한이 해결 되었습니다. 
- 새 클러스터 유형을 추가 `CLUSTER_TYPE = EXTERNAL` 고가용성에 대 한 가용성 그룹을 구성 합니다.
- 읽기 전용 라우팅을 위해 가용성 그룹 수신기를 수정 합니다.
- 조기 채택 프로그램 (EAP) 고객에 대 한 프로덕션 지원 합니다. 등록 [여기](http://aka.ms/eapsignup)합니다.

## <a name="ctp-14"></a>1.4 CTP

1.4 CTP 릴리스는 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- 활성화는 [SQL Server 에이전트](sql-server-linux-setup-sql-agent.md)합니다.
  - T-SQL 작업 기능을 사용할 수 있습니다.
- 고정된 표준 시간대 버그:
  - 표준 시간대 아시아/Kolkata 지원 합니다.
  - 고정된 getdate () 함수입니다.
- 비동기 네트워크 I / 0 개선 사항:
  - 메모리 내 OLTP 워크 로드 성능 크게 개선 되었습니다.
- 이제 docker 이미지 SQL Server 명령줄 유틸리티를 포함합니다. (sqlcmd/bcp)입니다.
- 백업에 대 한 지원 장치 VDI (Virtual Interface)를 사용할 수 있습니다.
- TempDB의 위치를 사용 하 여 설치 후 얻을 수 있습니다 `ALTER DATABASE`합니다.

## <a name="ctp-13"></a>1.3 CTP

1.3 CTP 릴리스는 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- 활성화 [전체 텍스트 검색](sql-server-linux-setup-full-text-search.md) 기능입니다.
- Always On 사용 [가용성 그룹 기능은](sql-server-linux-availability-group-overview.md) 고가용성에 대 한 합니다.
- 에 추가 된 기능 **mssql conf**:
  - 사용 하 여 첫 번째 시간 설정 **mssql conf**합니다. Mssql conf에서 사용 하는 참조는 [설치 가이드](sql-server-linux-setup.md#platforms)합니다.
  - 가용성 그룹을 사용 합니다. 참조는 [가용성 그룹 항목](sql-server-linux-availability-group-overview.md)합니다.
- 메모리 내 OLTP 파일 그룹에 대 한 고정된 네이티브 Linux 경로 지원 합니다.
- Dm_os_host_info DMV 기능을 사용할 수 있습니다.

## <a name="ctp-12"></a>1.2 CTP

1.2 CTP 릴리스는 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- 에 대 한 지원 [SUSE Linux Enterprise Server v12 SP2](quickstart-install-connect-suse.md)합니다.
- 코어 엔진 및 안정성 개선에 대 한 버그가 수정 되었습니다.
- Docker 이미지: 
  - 고정 [#1 발급](https://github.com/Microsoft/mssql-docker/issues/1) Python 이미지에 추가 하 여 합니다.
  - 제거 `/opt/mssql/data` 기본 볼륨으로 합니다.
- .NET 4.6.2 업데이트 됩니다.

## <a name="ctp-11"></a>CTP 1.1

CTP 1.1 릴리스에 다음과 같은 향상 된 기능 및 수정 포함 되어 있습니다.

- Red Hat Enterprise Linux 버전 7.3 지원 합니다.
- Ubuntu 16.10 지원 합니다.
- Ubuntu 16.04 업그레이드 된 Docker OS 레이어입니다.
- Docker 이미지에서 원격 분석 문제를 해결 합니다.
- SQL Server 설치 스크립트를 고정된 관련 버그입니다.
- 포함 하 여 고유 하 게 컴파일된 T-SQL 모듈에 대 한 향상 된 성능:
  - **OPENJSON**, **FOR JSON**, **JSON** 기본 제공 항목입니다.
  - 계산된 열 (인덱스만 사용 가능 비지속형 계산된 열에는 없지만 지속형된 계산된 열에서 메모리 내 테이블에 대 한).
  - **CROSS APPLY** 작업 합니다.
- 새로운 언어 기능:
  - 문자열 함수: **TRIM**, **CONCAT_WS**, **번역** 및 **STRING_AGG** 를 지 원하는 **WITHIN GROUP (ORDER BY)**합니다.
  - **대량 가져오기** 이제 CSV 형식 및 파일 원본으로 Azure Blob 저장소를 지원 합니다.

호환 모드 140:

- 비클러스터형 columnstore 인덱스의 경우에는 업데이트 성능이 향상 될 때 해당 행은 델타 저장소의 합니다. Delete에서 변경 및 삽입 작업을 업데이트 합니다. 또한 범위 좁히기 와이드에서 사용 하는 계획 모양을 변경 합니다.
- 일괄 처리 모드 쿼리는 이제 "메모리 피드백 루프를 부여 하는 데 사용"을 지원합니다. 이렇게 하면 동시성 및 일괄 처리 모드를 사용 하는 반복 되는 쿼리를 실행 하는 시스템에서 처리량 향상 됩니다. 따라서 더 많은 쿼리 그렇지 않은 경우 쿼리를 시작 하기 전에 메모리에 차단 하는 시스템에서 실행할 수 있습니다.
- 병렬 계획을 대신 columnstores에 대해 선택할 수 있도록 일괄 처리 모드 계획에 대 한 특정 계획을 무시 하 여 일괄 처리 모드 병렬 처리의 성능이 향상 되었습니다. 

[서비스 팩 1에서 향상 된 기능](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/) 이 CTP1.1 릴리스에서:
- CLR, Filestream/Filetable, 메모리 내 모드와 쿼리 저장소 개체에 대 한 복제 된 데이터베이스입니다.
- **만들** 또는 **ALTER** 프로그래밍 기능 개체에 대 한 연산자입니다.
- 새 **USE 힌트** 쿼리 옵션 쿼리 프로세서에 대 한 힌트를 제공할 수 있습니다. 자세히 보기: [쿼리 힌트](https://msdn.microsoft.com/en-us/library/ms181714.aspx)합니다.
- SQL 서비스 계정 이제 프로그래밍 방식으로 식별할 수 페이지 잠금 사용 메모리와 인스턴트 파일 초기화 사용 권한.
- TempDB 파일 수, 파일 크기 및 파일 증가 설정을 지원 합니다.
- XML 실행 계획에서 확장 된 진단 합니다.
- 간단한 연산자 쿼리 실행 프로 파일링 합니다.
- 새로운 동적 관리 함수인 **sys.dm_exec_query_statistics_xml**합니다.
- 증분 통계에 대 한 새 동적 관리 기능을 선택 합니다.
- 오류 로그에서 관련 로깅 메시지를 제거 잡음이 있는 메모리입니다.
- 향상 된 AlwaysOn 대기 시간 진단 합니다.
- 수동 변경 내용 추적 정리 했습니다.
- **DROP TABLE** 복제에 대 한 지원.
- **대량 삽입** 힙을에 **자동 TABLOCK** TF 715에서 합니다.
- 병렬 **삽입... 선택** 로컬 임시 테이블에 대 한 변경 합니다.

이러한 수정에 대 한 자세한 정보는 [서비스 팩 1 릴리스 설명](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)합니다.

향상 된 많은 데이터베이스 엔진 Windows와 Linux 모두에 적용 됩니다. Linux에서 현재 지원 되지 않는 데이터베이스 엔진 기능에 대 한 유일한 예외는 것입니다. 자세한 내용은 참조 [SQL Server 2017 (데이터베이스 엔진)의 새로운](https://msdn.microsoft.com/library/mt775028)합니다.

## <a name="see-also"></a>참고 항목

설치 요구 사항, 지원 되지 않는 기능 영역 및 알려진된 문제 [SQL Server 2017 linux에 대 한 릴리스 정보](sql-server-linux-release-notes.md)합니다.

