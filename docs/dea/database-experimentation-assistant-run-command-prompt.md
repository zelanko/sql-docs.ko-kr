---
title: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
description: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
ms.custom: seo-lt-2019
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: f2640e9018f29385851839932572aeaa3ee91ad9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "77600123"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>명령 프롬프트에서 데이터베이스 실험 도우미 실행

이 문서에서는 데이터베이스 실험 도우미 (DEA)에서 추적을 캡처한 다음 명령 프롬프트에서 결과를 모두 분석 하는 방법을 설명 합니다.

   > [!NOTE]
   > 각 DEA 작업에 대 한 자세한 내용을 보려면 다음 명령을 실행 하세요.
   >
   > `Deacmd.exe -o <operation> --help`
   >
   > 작업 이름은 필수입니다. 유효한 작업은 **분석**, **Startcapture**및 **stopcapture**입니다.

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>DEA 명령을 사용 하 여 새 워크 로드 캡처 시작

새 워크 로드 캡처를 시작 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

`Deacmd.exe -o StartCapture -h <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**예제**

`Deacmd.exe -o StartCapture -h localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

**추가 옵션**

`Deacmd.exe` 명령을 사용 하 여 새 워크 로드 캡처를 시작할 때 다음과 같은 추가 옵션을 사용할 수 있습니다.

| 옵션| 설명 |  
| --- | --- |
| -n, --name | 하다 추적 파일 이름 |
| -x,--형식 | 하다 추적 형식 (Trace = 0, Xevent = 1) |
| -d,--duration | 하다 캡처의 최대 지속 시간 (분) |
| -l, --location | 하다 호스트 컴퓨터에 추적/xevent 파일을 저장 하기 위한 출력 폴더의 위치입니다. |
| -t,--형식 | (기본값: 0) Sql Server의 유형/버전 (SqlServer = 0, AzureSQLDB = 1, Azure SQL Managed Instance = 2) |
| -h,--호스트 | 하다 캡처를 시작 하려면 호스트 이름 및/또는 인스턴스 이름을 SQL Server 하십시오. |
| -e,--암호화 | (기본값: True) SQL Server 인스턴스에 대 한 연결을 암호화 합니다. 기본값은 true입니다. |
| --신뢰 | (기본값: False) SQL Server 인스턴스에 연결 하는 동안 서버 인증서를 신뢰 합니다. 기본값은 false입니다. |
| -f,--databasename | (기본값:) 추적을 필터링 할 데이터베이스의 이름입니다. 지정 하지 않으면 모든 데이터베이스에서 캡처가 시작 됩니다. |
| -m,--authmode | (기본값: 0) 인증 모드 (Windows = 0, Sql 인증 = 1) |
| -u,--username | SQL Server에 연결 하기 위한 사용자 이름 |
| -p,--password | SQL Server에 연결 하기 위한 암호 |

## <a name="replay-a-workload-capture"></a>작업 캡처 재생

**Distributed Replay 사용**

Distributed Replay를 사용 하는 경우 다음 단계를 수행 합니다.

1. Distributed Replay 컨트롤러 컴퓨터에 로그인 합니다.
2. DEA 명령을 사용 하 여 캡처한 작업 추적을 IRF 파일로 변환 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. StartReplayCaptureTrace를 사용 하 여 SQL Server를 실행 하는 대상 컴퓨터에서 추적 캡처를 시작 합니다.

    a.  SSMS (SQL Server Management Studio)에서 <Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.을 엽니다.

    b.  지정 `Set @durationInMins=0` 된 시간이 지나면 추적 캡처가 자동으로 중지 되지 않도록를 실행 합니다.

    c.  추적 파일당 최대 파일 크기를 설정 하려면를 실행 `Set @maxfilesize`합니다. 권장 크기는 200 (MB)입니다.

    d.  추적 `@Tracefile` 파일에 대 한 고유한 이름을 설정 하려면 편집 합니다.

    e.  특정 `@dbname` 데이터베이스에 대해서만 작업을 캡처해야 하는 경우 데이터베이스 이름을 지정 하려면 편집 합니다. 기본적으로 전체 서버의 작업은 캡처됩니다.

4. 대상 SQL Server 인스턴스에 대해 IRF 파일을 재생 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  상태를 모니터링 하려면 명령 프롬프트에서를 실행 `DReplay status -f 1`합니다.

    b.  재생을 중지 하려면 (예: pass%가 예상 보다 낮은 것으로 표시 되는 경우) 명령 프롬프트에서를 실행 `DReplay cancel`합니다.

5. 대상 SQL Server 인스턴스에서 추적 캡처를 중지 합니다.
6. SSMS에서를 엽니다 `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`.
7. SQL Server `@Tracefile` 를 실행 하는 대상 컴퓨터의 추적 파일 경로와 일치 하도록 편집 합니다.
8. SQL Server를 실행 하는 대상 컴퓨터에 대해 스크립트를 실행 합니다.

**내장 재생 사용**

기본 제공 재생을 사용 하는 경우 Distributed Replay를 설정할 필요가 없습니다. 명령줄을 통해 제공 되는 재생 기능을 사용 하는 것은 가능 하지만, 중간에는 GUI를 사용 하 여 기본 제공 재생을 통해 재생을 실행할 수 있습니다.

## <a name="analyze-traces-using-the-dea-command"></a>DEA 명령을 사용 하 여 추적 분석

새 추적 분석을 시작 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -h <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**예제**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

이러한 추적 파일의 분석 보고서를 보려면 GUI를 사용 하 여 차트 및 구성 된 메트릭을 확인 해야 합니다.  그러나 분석 데이터베이스는 지정 된 SQL Server 인스턴스에 기록 되므로 생성 된 분석 테이블을 직접 쿼리할 수도 있습니다.

**추가 옵션**

DEA 명령을 사용 하 여 추적을 분석 하는 경우 다음과 같은 추가 옵션을 사용할 수 있습니다.

| 옵션| 설명 |  
| --- | --- |
| -a,--traceA | 하다 인스턴스에 대 한 이벤트 파일의 파일 경로입니다. 예 C:\traces\Sql2008trace.trc.  파일이 배치 되어 있으면 첫 번째 파일을 선택 하 고 DEA 롤오버 파일을 자동으로 확인 합니다. 파일이 blob에 있는 경우 이벤트 파일을 로컬에 저장 하려는 폴더 경로를 제공 합니다.  예 C:\traces\ |
| -b,--traceB | 하다 B 인스턴스에 대 한 이벤트 파일의 파일 경로입니다. 예 C:\traces\Sql2014trace.trc. 파일이 배치 되어 있으면 첫 번째 파일을 선택 하 고 DEA 롤오버 파일을 자동으로 확인 합니다. 파일이 blob에 있는 경우 이벤트 파일을 로컬에 저장 하려는 폴더 경로를 제공 합니다.  예 C:\traces\ |
| -r,--ReportName | 하다 현재 분석의 이름입니다. 생성 되는 분석 보고서는이 이름으로 식별 됩니다. |
| -t,--형식 | (기본값: 0) Sql Server의 유형/버전 (SqlServer = 0, AzureSQLDB = 1, Azure SQL Managed Instance = 2) |
| -h,--호스트 | 하다 SQL Server 호스트 이름 및/또는 인스턴스 이름 |
| -e,--암호화 | (기본값: True) SQL Server 인스턴스에 대 한 연결을 암호화 합니다. 기본값은 true입니다. |
| --신뢰 | (기본값: False) SQL Server 인스턴스에 연결 하는 동안 서버 인증서를 신뢰 합니다. 기본값은 false입니다. |
| -m,--authmode | (기본값: 0) 인증 모드 (Windows = 0, Sql 인증 = 1) |
| -u,--username | SQL Server에 연결 하기 위한 사용자 이름 |
| --p | SQL Server에 연결 하기 위한 암호 |
| --ab | (기본값: False) 추적 A의 저장소 위치가 blob에 있습니다. 을 사용 하는 경우--아부다비 (Blob Url 추적)도 지정 해야 합니다. |
| --bb | (기본값: False) 추적 B의 저장소 위치가 blob에 있습니다. 사용 되는 경우--bbu (추적 B Blob Url)도 지정 해야 합니다. |
| --아부다비 | SAS 키가 있는 인스턴스의 Blob URL |
| --bbu | SAS 키가 포함 된 B 인스턴스의 Blob URL |

## <a name="see-also"></a>참고 항목

- DEA 사용에 대 한 자세한 내용은 [데이터베이스 실험 도우미 개요](database-experimentation-assistant-overview.md)를 참조 하세요.
