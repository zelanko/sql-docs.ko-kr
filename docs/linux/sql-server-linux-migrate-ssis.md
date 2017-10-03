---
title: "추출, 변환 및 SSIS와 Linux에서 데이터를 로드 | Microsoft Docs"
description: 
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: aa4ac0cca739ea57a28beb399325d55b38502217
ms.contentlocale: ko-kr
ms.lasthandoff: 10/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>추출, 변환 및 SSIS와 Linux에서 데이터 로드

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 Linux에서 SQL Server Integration Services (SSIS) 패키지를 실행 하는 방법에 설명 합니다. 여러 소스 및 형식 중에서 데이터를 추출 하 여 복잡 한 데이터 통합 문제를 해결 하는 SSIS 변환 및 데이터를 정리 하 고 여러 대상에 데이터를 로드 합니다. 

Linux에서 실행 되는 SSIS 패키지는 linux 또는 Docker에서 클라우드에서 또는 Windows 온-프레미스에서 실행 중인 Microsoft SQL Server에 연결할 수 있습니다. 또한 Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, ODBC 데이터 원본, 플랫 파일 및 ADO.NET 원본, XML 파일 및 OData 서비스 등의 다른 데이터 원본에 연결할 수 있습니다.

SSIS의 기능에 대 한 자세한 내용은 참조 하십시오. [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

Linux 컴퓨터에서 SSIS 패키지를 실행 하려면 먼저 SQL Server Integration Services를 설치 해야 합니다. SSIS는 Linux 컴퓨터의 SQL Server 설치에 포함 되지 않습니다. 설치 지침을 참조 하십시오. [SQL Server Integration Services 설치](sql-server-linux-setup-ssis.md)합니다.

Windows 컴퓨터를 만들고 패키지를 유지 관리할 수도 있습니다. SSIS 디자인 및 관리 도구는 현재 Linux 컴퓨터에 사용할 수 없는 Windows 응용 프로그램. 

## <a name="run-an-ssis-package"></a>SSIS 패키지를 실행 합니다.

Linux 컴퓨터에서 SSIS 패키지를 실행 하려면 다음 작업을 수행 합니다.

1.  Linux 컴퓨터에 SSIS 패키지를 복사 합니다.
2.  다음 명령을 실행합니다.
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="other-common-ssis-tasks"></a>다른 일반적인 SSIS 작업

-   **패키지를 디자인**합니다.

    -   **ODBC 데이터 원본에 연결**합니다. 이상 Linux CTP 2.1 새로 고침에서 SSIS, SSIS 패키지는 Linux 기반 ODBC 연결 사용할 수 있습니다. 이 기능은 SQL Server 및 MySQL ODBC 드라이버와 함께 테스트 되었습니다 하지만 또한 ODBC 사양을 따르는 모든 유니코드 ODBC 드라이버와 함께 사용 해야 합니다. 디자인 타임에 ODBC 데이터;에 연결 하는 DSN 또는 연결 문자열 중 하나를 제공할 수 있습니다. 또한 Windows 인증을 사용할 수 있습니다. 자세한 내용은 참조는 [블로그 게시물 Linux ODBC 지원 발표](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)합니다.

    -   **경로**합니다. SSIS 패키지에서 Windows 스타일 경로 제공 합니다. SSIS Linux에서 Linux 스타일 경로의 지원 하지 않지만 실행 시 Windows 스타일 경로의 Linux 스타일 경로에 매핑합니다. 그런 다음, 예를 들어 매핑합니다 Windows 스타일 경로 Linux에서 SSIS `C:\test` Linux 스타일 경로에 `/test`합니다.

-   **패키지 배포**합니다. 이 릴리스에서 Linux에서 파일 시스템에만 패키지를 저장할 수 있습니다. SSIS 카탈로그 데이터베이스와 레거시 SSIS 서비스 패키지 배포 및 저장을 위해 Linux에서 사용할 수 없는 경우

-   **패키지 예약**합니다. 일정 도구와 같은 Linux 시스템을 사용 하면 `cron` 패키지를 예약 하 합니다. 이 릴리스에서 패키지 실행을 예약 Linux에서 SQL 에이전트를 사용할 수 없습니다. 자세한 내용은 참조 하십시오. [cron 사용 하 여 Linux에서 일정 SSIS 패키지](sql-server-linux-schedule-ssis-packages.md)합니다.

## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진된 문제

### <a name="general-limitations-and-known-issues"></a>일반적인 제한 사항 및 알려진된 문제

Linux에서 SSIS의이 릴리스에서 다음과 같은 기능이 지원 되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약 된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS 규모 확장
  - SSIS 용 azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

다른 제한 사항 및 Linux에서 SSIS의 알려진된 문제에 대 한 참조는 [릴리스 정보](sql-server-linux-release-notes.md#ssis)합니다.

### <a name="components"></a>지원 되는 / 지원 되지 않는 구성 요소

다음 기본 제공 Integration Services 구성 요소는 Linux에서 지원 됩니다. 그 중 일부는 다음 표에 설명 된 대로 Linux 플랫폼에는 제한이 있습니다.

여기에 나열 되지 않은 기본 제공 구성 요소는 Linux에서 지원 되지 않습니다.

#### <a name="supported-control-flow-tasks"></a>제어 흐름 태스크를 지원합니다.
- 대량 삽입 태스크
- 데이터 흐름 태스크
- 데이터 프로파일링 태스크
- SQL 실행 태스크
- T-SQL 문 실행 태스크
- 식 태스크
- FTP 태스크
- 웹 서비스 태스크
- XML 태스크

#### <a name="control-flow-tasks-supported-with-limitations"></a>제어 흐름 작업 제한 사항과 함께 지원

| 태스크 | 제한 사항 |
|------------|---|
| 프로세스 실행 태스크 | 만 in-process 모드를 지원합니다. |
| 파일 시스템 태스크 | *이동 디렉터리* 및 *파일 특성을 설정할* 동작은 지원 되지 않습니다. |
| 스크립트 태스크 | 표준.NET Framework Api만 지원합니다. |
| 메일 보내기 태스크 | 익명 사용자 모드에만 지원합니다. |
| 데이터베이스 전송 태스크 | UNC 경로는 지원되지 않습니다. |
| | |

#### <a name="supported-control-flow-containers"></a>제어 흐름 컨테이너를 지원합니다.
- 시퀀스 컨테이너
- For 루프 컨테이너
- Foreach 루프 컨테이너

#### <a name="supported-data-flow-sources-and-destinations"></a>지원 되는 데이터 흐름 원본 및 대상
- 원시 파일 원본 및 대상
- XML 원본

#### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>데이터 흐름 원본 및 대상을 제한 사항과 함께 지원

| 구성 요소 | 제한 사항 |
|------------|---|
| ADO.NET 원본 및 대상 | SQLClient 데이터 공급자만 지원 합니다. |
| 플랫 파일 원본 및 대상 | 기본 경로 매핑 규칙이 적용 되는 Windows 스타일 파일 경로 지원 합니다. 예를 들어 `D:\home\ssis\travel.csv` 되 `/home/ssis/travel.csv`합니다. |
| OData 원본 | 기본 인증에만 지원합니다. |
| ODBC 원본 및 대상 | Linux에서 64 비트 유니코드 ODBC 드라이버를 지원합니다. Linux에서 UnixODBC 드라이버 관리자에 따라 다릅니다. |
| OLE DB 원본 및 대상 | SQL Server에 대 한 SQL Server Native Client 11.0 및 Microsoft OLE DB Provider를만 지원 합니다. |
| | |

#### <a name="supported-data-flow-transformations"></a>데이터 흐름 변환 지원
- 집계
- 감사
- 분산 데이터 배포자
- 문자표 변환
- 조건부 분할
- 열 복사
- 데이터 변환
- 파생 열
- 열 내보내기
- 유사 항목 그룹화
- 유사 항목 조회
- 열 가져오기
- 조회
- 병합
- 병합 조인
- 멀티 캐스트
- 피벗
- 행 개수
- 느린 변경 차원
- 정렬
- 용어 조회
- Union All
- 피벗 해제

#### <a name="data-flow-transformations-supported-with-limitations"></a>데이터 흐름 변환 제한 사항과 함께 지원

| 구성 요소 | 제한 사항 |
|------------|---|
| OLE DB 명령 변환 | OLE DB 원본 및 대상으로 동일한 제한 사항이 있습니다. |
| 스크립트 구성 요소 | 표준.NET Framework Api만 지원합니다. |
| | |

### <a name="supported-and-unsupported-log-providers"></a>지원 되는 / 지원 되지 않는 로그 공급자
기본 제공 SSIS 로그 공급자는 Linux에서 지원 되는 모든 Windows 이벤트 로그 공급자를 제외 하 고 있습니다.

SQL Server 로그 공급자는 SQL 인증만 지원 합니다. Windows 인증을 지원 하지는 않습니다.

텍스트 파일, XML 파일 및 SQL Server Profiler 용 SSIS 로그 공급자는 사용자가 지정한 파일에 해당 출력을 씁니다. 파일 경로에 다음 고려 사항이 적용 됩니다.
-   경로 제공 하지 않으면 로그 공급자는 호스트의 현재 디렉터리에 씁니다. 현재 사용자는 호스트의 현재 디렉터리에 쓸 수 있는 권한이 없으면 로그 공급자에서 오류가 발생 합니다.
-   파일 경로에 환경 변수를 사용할 수 없습니다. 환경 변수를 지정 하면 지정 하는 리터럴 텍스트 파일 경로에 나타납니다. 예를 들어, 지정 하는 경우 `%TMP%/log.txt`, 로그 공급자에 리터럴 텍스트를 추가 `/%TMP%/log.txt` 현재 호스트 디렉터리에 있습니다.

## <a name="more-info-about-ssis-on-linux"></a>Linux에서 SSIS에 대 한 자세한 정보

Linux에서 SSIS에 대 한 자세한 내용은 다음 블로그 게시물을 참조 합니다.

-   [Linux에서 SSIS는 SQL Server 2017 CTP2.1에서 사용할 수 있는](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC는 SSIS (SQL Server 2017 CTP 2.1 새로 고침)를 linux에서 지원](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>SSIS에 대 한 자세한 정보

Microsoft SQL Server Integration Services (SSIS)는 추출, 변환 및 로드 (ETL) 패키지의 데이터 웨어하우징를 포함 하 여 고성능 데이터 통합 솔루션을 구축 하기 위한 플랫폼입니다. SSIS에 대한 자세한 내용은 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md)를 참조하세요.

SSIS에는 다음과 같은 기능이 포함 됩니다.
- 그래픽 도구 및 Windows에서 패키지 작성 및 디버깅에 대 한 마법사
- 다양 한 FTP 작업과 같은 워크플로 기능을 수행 하 고 SQL 문을 실행 하며 전자 메일 메시지 보내기 작업
- 다양 한 데이터 원본 및 대상 데이터 추출 및 로드에 대 한
- 다양 한 정리, 집계, 병합 및 데이터 복사를 위한 변환
- 사용자 고유의 사용자 지정 스크립트 및 구성 요소와 SSIS를 확장 하기 위한 응용 프로그래밍 인터페이스 (Api)

SSIS와 시작 하려면 최신 버전의 다운로드 [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md)합니다.

## <a name="see-also"></a>참고 항목
- [SQL Server Integration Services에 대 한 자세한 정보](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) 개발 및 관리 도구](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 자습서](../integration-services/integration-services-tutorials.md)

