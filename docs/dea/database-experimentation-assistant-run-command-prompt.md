---
title: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
description: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
ms.custom: seo-lt-2019
ms.date: 01/24/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 8055ae8b66c2f2b59f18b0ee40dcac8753c0eb7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "76831756"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>명령 프롬프트에서 데이터베이스 실험 도우미 실행

이 문서에서는 데이터베이스 실험 도우미 (DEA)에서 추적을 캡처한 다음 명령 프롬프트에서 결과를 모두 분석 하는 방법을 설명 합니다.

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>DEA 명령을 사용 하 여 새 워크 로드 캡처 시작

새 워크 로드 캡처를 시작 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**예제**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload-capture"></a>작업 캡처 재생

1. Distributed Replay 컨트롤러 컴퓨터에 로그인 합니다.
2. DEA 명령을 사용 하 여 캡처한 작업 추적을 IRF 파일로 변환 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. StartReplayCaptureTrace를 사용 하 여 SQL Server를 실행 하는 대상 컴퓨터에서 추적 캡처를 시작 합니다.

    a.  SSMS (SQL Server Management Studio)에서 <Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.을 엽니다.

    b.  지정 `Set @durationInMins=0` 된 시간이 지나면 추적 캡처가 자동으로 중지 되지 않도록를 실행 합니다.

    다.  추적 파일당 최대 파일 크기를 설정 하려면를 실행 `Set @maxfilesize`합니다. 권장 크기는 200 (MB)입니다.

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

## <a name="analyze-traces-using-the-dea-command"></a>DEA 명령을 사용 하 여 추적 분석

새 추적 분석을 시작 하려면 명령 프롬프트에서 다음 명령을 실행 합니다.

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**예제**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="see-also"></a>참고 항목

- DEA 사용에 대 한 자세한 내용은 [데이터베이스 실험 도우미 개요](database-experimentation-assistant-overview.md)를 참조 하세요.
