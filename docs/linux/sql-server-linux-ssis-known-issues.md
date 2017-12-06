---
title: "Linux에서 SSIS에 대 한 알려진된 문제 및 제한 | Microsoft Docs"
description: "이 문서에서는 설명 제한 사항 및 알려진된 문제 SQL Server Integration Services (SSIS)에 대 한 Linux 컴퓨터에서"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 96bf588edd15c77caa6649ac04b6a95046135e95
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Linux에서 SSIS에 대 한 알려진된 문제 및 제한

이 항목에서는 현재 제한 사항 및 알려진된 문제 SQL Server Integration Services (SSIS)에 대 한 linux.

## <a name="general-limitations-and-known-issues"></a>일반적인 제한 사항 및 알려진된 문제

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

## <a name="components"></a>지원 되는 / 지원 되지 않는 구성 요소

다음 기본 제공 Integration Services 구성 요소는 Linux에서 지원 됩니다. 그 중 일부는 다음 표에 설명 된 대로 Linux 플랫폼에는 제한이 있습니다.

여기에 나열 되지 않은 기본 제공 구성 요소는 Linux에서 지원 되지 않습니다.

### <a name="supported-control-flow-tasks"></a>제어 흐름 태스크를 지원합니다.
- 대량 삽입 태스크
- 데이터 흐름 태스크
- 데이터 프로파일링 태스크
- SQL 실행 태스크
- T-SQL 문 실행 태스크
- 식 태스크
- FTP 태스크
- 웹 서비스 태스크
- XML 태스크

### <a name="control-flow-tasks-supported-with-limitations"></a>제어 흐름 작업 제한 사항과 함께 지원

| 태스크 | 제한 사항 |
|------------|---|
| 프로세스 실행 태스크 | 만 in-process 모드를 지원합니다. |
| 파일 시스템 태스크 | *이동 디렉터리* 및 *파일 특성을 설정할* 동작은 지원 되지 않습니다. |
| 스크립트 태스크 | 표준.NET Framework Api만 지원합니다. |
| 메일 보내기 태스크 | 익명 사용자 모드에만 지원합니다. |
| 데이터베이스 전송 태스크 | UNC 경로는 지원되지 않습니다. |
| | |

### <a name="supported-control-flow-containers"></a>제어 흐름 컨테이너를 지원합니다.
- 시퀀스 컨테이너
- For 루프 컨테이너
- Foreach 루프 컨테이너

### <a name="supported-data-flow-sources-and-destinations"></a>지원 되는 데이터 흐름 원본 및 대상
- 원시 파일 원본 및 대상
- XML 원본

### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>데이터 흐름 원본 및 대상을 제한 사항과 함께 지원

| 구성 요소 | 제한 사항 |
|------------|---|
| ADO.NET 원본 및 대상 | SQLClient 데이터 공급자만 지원 합니다. |
| 플랫 파일 원본 및 대상 | 기본 경로 매핑 규칙이 적용 되는 Windows 스타일 파일 경로 지원 합니다. 예를 들어 `D:\home\ssis\travel.csv` 되 `/home/ssis/travel.csv`합니다. |
| OData 원본 | 기본 인증에만 지원합니다. |
| ODBC 원본 및 대상 | Linux에서 64 비트 유니코드 ODBC 드라이버를 지원합니다. Linux에서 UnixODBC 드라이버 관리자에 따라 다릅니다. |
| OLE DB 원본 및 대상 | SQL Server에 대 한 SQL Server Native Client 11.0 및 Microsoft OLE DB Provider를만 지원 합니다. |
| | |

### <a name="supported-data-flow-transformations"></a>데이터 흐름 변환 지원
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

### <a name="data-flow-transformations-supported-with-limitations"></a>데이터 흐름 변환 제한 사항과 함께 지원

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

