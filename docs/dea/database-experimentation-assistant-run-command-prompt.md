---
title: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
description: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
ms.custom: seo-lt-2019
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: c3b87eafa460cfef69666a3837f56626dab81d47
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056570"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt-sql-server"></a>명령 프롬프트에서 데이터베이스 실험 도우미 실행 (SQL Server)

이 문서에서는 명령 프롬프트 창을 사용 하 여 데이터베이스 실험 도우미 (DEA)에서 추적을 캡처한 다음 결과를 분석 하는 방법을 설명 합니다. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>DEA 명령을 사용 하 여 새 워크 로드 캡처 시작

새 워크 로드 캡처를 시작 하려면 다음 명령을 실행 합니다.

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**예제**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>작업 재생

1.  Distributed Replay 컨트롤러 컴퓨터에 로그인 합니다.
2.  DEA 명령을 사용 하 여 캡처한 작업 추적을 IRF 파일로 변환 합니다.

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  StartReplayCaptureTrace를 사용 하 여 SQL Server를 실행 하는 대상 컴퓨터에서 추적 캡처를 시작 합니다.
       
    a.  SSMS (SQL Server Management Studio)에서 < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql.를 엽니다.
    
    b.  지정 된 시간이 지나면 추적 캡처가 자동으로 중지 되지 않도록 `Set @durationInMins=0`를 실행 합니다.
    
    c.  추적 파일당 최대 파일 크기를 설정 하려면 `Set @maxfilesize`를 실행 합니다. 권장 크기는 200 (MB)입니다.
    
    d.  추적 파일에 대 한 고유한 이름을 설정 하려면 `@Tracefile`를 편집 합니다.
    
    e.  특정 데이터베이스 에서만 워크 로드를 캡처해야 하는 경우 데이터베이스 이름을 지정 하려면 `@dbname`를 편집 합니다. 기본적으로 전체 서버의 작업은 캡처됩니다. 
4.  대상 SQL Server 인스턴스에 대해 IRF 파일을 재생 합니다.

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  상태를 모니터링 하려면 명령 프롬프트 창을 열고 `DReplay status -f 1`를 실행 합니다.
        
    b.  통과%가 예상 보다 낮은 것으로 표시 되는 경우와 같이 재생을 중지 하려면 명령 프롬프트 창을 열고 `DReplay cancel`를 실행 합니다.

5.  대상 SQL Server 인스턴스에서 추적 캡처를 중지 합니다.
6.  SSMS에서 `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`를 엽니다.
7.  SQL Server를 실행 하는 대상 컴퓨터의 추적 파일 경로와 일치 하도록 `@Tracefile`를 편집 합니다.
8.  SQL Server를 실행 하는 대상 컴퓨터에 대해 스크립트를 실행 합니다.

## <a name="analyze-traces-by-using-the-dea-command"></a>DEA 명령을 사용 하 여 추적 분석

새 추적 분석을 시작 하려면 다음 명령을 실행 합니다.

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**예제**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>다음 단계

DEA 및 데모에 대 한 19 분의 소개는 다음 비디오를 시청 하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
