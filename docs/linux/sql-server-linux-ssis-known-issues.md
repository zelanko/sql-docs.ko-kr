---
title: Linux SSIS의 제한 사항 및 알려진 문제
description: 이 문서에서는 Linux 컴퓨터의 SSIS(SQL Server Integration Services)에 대한 제한 사항과 알려진 문제를 설명합니다.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 45e5d9b36b6fd75db7bbc3c5ea397ee9226e2771
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288067"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Linux SSIS의 제한 사항 및 알려진 문제

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux의 SSIS(SQL Server Integration Services)에 대한 제한 사항과 알려진 문제를 설명합니다.

## <a name="general-limitations-and-known-issues"></a>일반적인 제한 사항 및 알려진 문제

Linux 기본 SSIS의 이번 릴리스에서는 다음 기능이 지원되지 않습니다.
  - SSIS 카탈로그 데이터베이스
  - SQL 에이전트에서 예약된 패키지 실행
  - Windows 인증
  - 타사 구성 요소
  - CDC(변경 데이터 캡처)
  - SSIS Scale Out
  - SSIS용 Azure 기능 팩
  - Hadoop 및 HDFS 지원
  - Microsoft Connector for SAP BW

Linux의 SSIS에 대한 다른 제한 사항과 알려진 문제는 [릴리스 정보](sql-server-linux-release-notes.md#ssis)를 참조하세요.

## <a name="supported-and-unsupported-components"></a><a name="components"></a> 지원되는/지원되지 않는 구성 요소

Linux에서 지원되는 기본 제공 Integration Services 구성 요소는 다음과 같습니다. 구성 요소 중 일부에는 Linux 플랫폼에 대한 제한이 있습니다. 여기에 나열되지 않은 기본 제공 구성 요소는 Linux에서 지원되지 않습니다.

## <a name="supported-control-flow-tasks"></a>지원되는 제어 흐름 작업
- 대량 삽입 태스크
- 데이터 흐름 태스크
- 데이터 프로파일링 태스크
- SQL 실행 태스크
- T-SQL 문 실행 태스크
- 식 태스크
- FTP 태스크
- 웹 서비스 태스크
- XML 태스크

## <a name="control-flow-tasks-supported-with-limitations"></a>제한적으로 지원되는 제어 흐름 작업

| Task | 제한 사항 |
|------------|---|
| 프로세스 실행 태스크 | In Process 모드만 지원합니다. |
| 파일 시스템 태스크 | *디렉터리 이동* 및 *파일 특성 설정* 작업은 지원되지 않습니다. |
| 스크립트 태스크 | 표준 .NET Framework API만 지원합니다. |
| 메일 보내기 태스크 | 익명 사용자 모드만 지원합니다. |
| 데이터베이스 전송 작업 | UNC 경로는 지원되지 않습니다. |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>지원되는/지원되지 않는 유지 관리 계획 작업

SQL Server 유지 관리 계획에서 일반적으로 다양한 SSIS 작업을 사용할 수 있습니다.

다음 유지 관리 계획 작업은 Linux에서 지원되지 않습니다.
- 운영자에게 알림
- SQL Server 에이전트 작업 실행

다음 유지 관리 계획 작업은 Linux에서 지원됩니다.
- 데이터베이스 무결성 검사
- 데이터베이스 축소
- 인덱스 다시 구성
- 인덱스 다시 작성
- 통계 업데이트
- 기록 정리
- 데이터베이스 백업
- T-SQL 문

## <a name="supported-control-flow-containers"></a>지원되는 제어 흐름 컨테이너
- 시퀀스 컨테이너
- For 루프 컨테이너
- Foreach 루프 컨테이너

## <a name="supported-data-flow-sources-and-destinations"></a>지원되는 데이터 흐름 원본 및 대상
- 원시 파일 원본 및 대상
- XML 원본

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>제한적으로 지원되는 데이터 흐름 원본 및 대상

| 구성 요소 | 제한 사항 |
|------------|---|
| ADO.NET 원본 및 대상 | SQLClient 데이터 공급자만 지원합니다. |
| 플랫 파일 원본 및 대상 | 기본 경로 매핑 규칙이 적용되는 Windows 스타일 파일 경로만 지원합니다. 예를 들어 `D:\home\ssis\travel.csv`는 `/home/ssis/travel.csv`가 됩니다. |
| OData 원본 | 기본 인증만 지원합니다. |
| ODBC 원본 및 대상 | Linux에서 64비트 유니코드 ODBC 드라이버를 지원합니다. Linux의 UnixODBC 드라이버 관리자에 따라 달라집니다. |
| OLE DB 원본 및 대상 | SQL Server Native Client 11.0 및 Microsoft OLE DB Provider for SQL Server만 지원합니다. |
| | |

## <a name="supported-data-flow-transformations"></a>지원되는 데이터 흐름 변환
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
- 멀티캐스트
- 피벗
- 행 개수
- 느린 변경 차원
- 정렬
- 용어 조회
- Union All
- 피벗 해제

## <a name="data-flow-transformations-supported-with-limitations"></a>제한적으로 지원되는 데이터 흐름 변환

| 구성 요소 | 제한 사항 |
|------------|---|
| OLE DB 명령 변환 | OLE DB 원본 및 대상과 동일한 제한 사항입니다. |
| 스크립트 구성 요소 | 표준 .NET Framework API만 지원합니다. |
| | |

## <a name="supported-and-unsupported-log-providers"></a>지원되는/지원되지 않는 로그 공급자
Windows 이벤트 로그 공급자를 제외하고 모든 기본 제공 SSIS 로그 공급자가 Linux에서 지원됩니다.

SQL Server 로그 공급자는 SQL 인증만 지원합니다. Windows 인증은 지원하지 않습니다.

텍스트 파일, XML 파일 및 SQL Server Profiler에 대한 SSIS 로그 공급자는 지정한 파일에 출력을 씁니다. 파일 경로에 적용되는 고려 사항은 다음과 같습니다.
-   경로를 제공하지 않으면 로그 공급자는 호스트의 현재 디렉터리에 씁니다. 현재 사용자에게 호스트의 현재 디렉터리에 대한 쓰기 권한이 없는 경우 로그 공급자는 오류를 발생시킵니다.
-   파일 경로에는 환경 변수를 사용할 수 없습니다. 환경 변수를 지정하면 지정한 리터럴 텍스트가 파일 경로에 표시됩니다. 예를 들어 `%TMP%/log.txt`를 지정하면 로그 공급자는 현재 호스트 디렉터리에 리터럴 텍스트 `/%TMP%/log.txt`를 추가합니다.

## <a name="related-content-about-ssis-on-linux"></a>Linux SSIS에 대한 관련 콘텐츠
-   [SSIS를 사용하여 Linux에서 데이터 추출, 변환 및 로드](sql-server-linux-migrate-ssis.md)
-   [Linux에서 SSIS(SQL Server Integration Services) 설치](sql-server-linux-setup-ssis.md)
-   [ssis-conf를 사용하여 Linux에서 SQL Server Integration Services 구성](sql-server-linux-configure-ssis.md)
-   [cron을 사용하여 Linux에서 SQL Server Integration Services 패키지 실행 예약](sql-server-linux-schedule-ssis-packages.md)
