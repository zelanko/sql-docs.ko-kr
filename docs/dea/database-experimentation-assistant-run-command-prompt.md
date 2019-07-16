---
title: SQL Server 업그레이드에 대 한 명령 프롬프트에서 데이터베이스 실험 도우미 실행
description: 명령 프롬프트에서 데이터베이스 실험 도우미 실행
ms.custom: ''
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
ms.openlocfilehash: 475c3dc1366e69dbc164547bbf5dfc8c06515c56
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050474"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>명령 프롬프트에서 데이터베이스 실험 도우미 실행

이 문서에서는 명령 프롬프트 창을 사용 하 여 추적에서 데이터베이스 실험 도우미 (비활성화)를 캡처하고 결과 분석 하는 방법을 설명 합니다. 

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>새 워크 로드 캡처를 비활성화 명령을 사용 하 여 시작

새 워크 로드 캡처를 시작 하려면 다음 명령을 실행 합니다.

`Deacmd.exe -o startcapturetrace -s <SQLServerInstance> -e <encryptconnection> -u <trustservercertificate> -d <database name> -p <trace file path> -f <trace file name> -t <Max duration>`

**예제**

`Deacmd.exe -o startcapturetrace -s localhost -e -d adventureworks -p c:\test -f sql2008capture -t 60`

## <a name="replay-a-workload"></a>작업 재생

1.  Distributed Replay 컨트롤러 컴퓨터에 로그인 합니다.
2.  IRF 파일로 비활성화 명령을 사용 하 여 캡처되는 작업 추적을 변환 합니다.

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3.  StartReplayCaptureTrace.sql를 사용 하 여 SQL Server를 실행 하는 대상 컴퓨터에서 추적 캡처를 시작 합니다.
       
    a.  SSMS SQL Server Management Studio ()를 열고 < Dea_InstallPath\>\Scripts\StartReplayCaptureTrace.sql 합니다.
    
    b.  실행 `Set @durationInMins=0` 추적 캡처는 지정된 된 시간 후 자동으로 중지 하지 않도록 합니다.
    
    c.  추적 파일 당 최대 파일 크기를 설정 하려면 실행 `Set @maxfilesize`합니다. 권장된 크기는 mb 단위로 200입니다.
    
    d.  편집 `@Tracefile` 추적 파일의 고유 이름을 설정 하도록 합니다.
    
    e.  편집 `@dbname` 특정 데이터베이스에만 작업을 캡처해야 하는 경우 데이터베이스 이름을 지정 합니다. 전체 서버에서 워크 로드는 기본적으로 캡처됩니다. 
4.  재생 대상 SQL Server 인스턴스에 대해 IRF 파일:

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`
        
    a.  상태를 모니터링 하려면 명령 프롬프트 창을 열고 실행 `DReplay status -f 1`합니다.
        
    b.  재생을 중지 하려면 같은 통과 비율은 예상 보다 낮은 것이 표시 하는 경우 명령 프롬프트 창을 열고 실행 `DReplay cancel`합니다.

5.  대상 SQL Server 인스턴스에서 추적 캡처를 중지 합니다.
6.  SSMS를 열고 `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql`합니다.
7.  편집 `@Tracefile` SQL Server를 실행 하는 대상 컴퓨터에서 추적 파일 경로 일치 합니다.
8.  SQL Server를 실행 하는 대상 컴퓨터에 대 한 스크립트를 실행 합니다.

## <a name="analyze-traces-by-using-the-dea-command"></a>비활성화 명령을 사용 하 여 추적을 분석

새 추적 분석을 시작 하려면 다음 명령을 실행 합니다.

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -s <SQLserverInstance> -e <encryptconnection> -u <trustservercertificate>`

**예제**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -s localhost -e`

## <a name="next-steps"></a>다음 단계

비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
