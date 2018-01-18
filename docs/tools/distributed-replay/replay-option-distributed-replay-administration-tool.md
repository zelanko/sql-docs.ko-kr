---
title: "재생 옵션 (Distributed Replay Administration Tool) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: distributed-replay
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7bce6a5-d414-488d-a3cd-50c1c62019c4
caps.latest.revision: "25"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf93f19d25faf48efa3195d7d34348354eae5969
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="replay-option-distributed-replay-administration-tool"></a>재생 옵션(Distributed Replay Administration Tool)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 관리 도구인 **DReplay.exe**, distributed replay controller와 통신 하는 데 사용할 수 있는 명령줄 도구입니다. 이 항목에서는 **replay** 명령줄 옵션과 해당 구문에 대해 설명합니다.  
  
 **replay** 옵션은 이벤트 재생 단계를 시작합니다. 이 단계에서 컨트롤러는 재생 데이터를 지정된 클라이언트로 발송하고 분산 재생을 시작하며 클라이언트를 동기화합니다. 필요에 따라 재생에 참여하는 각 클라이언트는 재생 작업을 기록하고 결과 추적 파일을 로컬에 저장할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") 관리 도구 구문과 함께 사용 되는 구문 표기 규칙에 대 한 자세한 내용은 참조 하십시오. [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>구문  
  
```  
  
dreplay replay [-m controller] -d controller_working_dir [-o]  
    [-s target_server] -w clients [-c config_file]  
    [-f status_interval]  
```  
  
#### <a name="parameters"></a>매개 변수  
 **-m** *controller*  
 컨트롤러의 컴퓨터 이름을 지정합니다. "`localhost`" 또는 "`.`"을 사용하여 로컬 컴퓨터를 참조할 수 있습니다.  
  
 **-m** 매개 변수를 지정하지 않으면 로컬 컴퓨터가 사용됩니다.  
  
 **-d** *controller_working_dir*  
 컨트롤러에서 중간 파일이 저장될 디렉터리를 지정합니다. **-d** 매개 변수는 필수 항목입니다.  
  
 적용되는 요구 사항은 다음과 같습니다.  
  
-   디렉터리가 컨트롤러에 있어야 합니다.  
  
-   드라이브 문자로 시작하는 전체 경로(예: `c:\WorkingDir`)를 지정해야 합니다.  
  
-   경로가 백슬래시("`\`")로 끝나지 않아야 합니다.  
  
-   UNC 경로는 지원되지 않습니다.  
  
 **-o**  
 클라이언트의 재생 작업을 캡처하여 클라이언트 구성 파일 `<ResultDirectory>` 의 `DReplayClient.xml`요소에 지정된 경로에 있는 결과 추적 파일에 저장합니다.  
  
 **–o** 매개 변수를 지정하지 않으면 결과 추적 파일이 생성되지 않습니다. 콘솔 출력은 재생이 끝날 때 요약 정보를 반환하지만 그 외 다른 재생 통계는 사용할 수 없습니다.  
  
 **-s** *target_server*  
 분산 작업이 재생될 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정합니다. 이 매개 변수는 **server_name[\인스턴스 이름]**형식으로 지정해야 합니다.  
  
 "`localhost`" 또는 "`.`"을 대상 서버로 사용할 수 없습니다.  
  
 재생 구성 파일 **의** 섹션에 `<Server>` 요소가 지정되어 있으면 `<ReplayOptions>` -s `DReplay.exe.replay.config`매개 변수를 지정할 필요가 없습니다.  
  
 **-s** 매개 변수를 사용하는 경우 재생 구성 파일의 `<Server>` 섹션에 있는 `<ReplayOptions>` 요소가 무시됩니다.  
  
 **-w** *clients*  
 이 필수 매개 변수는 분산 재생에 참여할 클라이언트의 컴퓨터 이름을 지정하는 쉼표로 구분된 목록(공백 없음)입니다. IP 주소는 허용되지 않습니다. 클라이언트가 컨트롤러에 이미 등록되어 있어야 합니다.  
  
> [!NOTE]  
>  각 클라이언트는 클라이언트 서비스가 시작될 때 클라이언트 구성 파일에 지정된 컨트롤러에 등록됩니다.  
  
 **-c** *config_file*  
 재생 구성 파일의 전체 경로이며, 다른 위치에 저장된 경우 파일의 위치를 지정하는 데 사용됩니다.  
  
 재생 구성 파일 **의 기본값을 사용하려는 경우** -c `DReplay.exe.replay.config`매개 변수를 지정할 필요가 없습니다.  
  
 **-f** *status_interval*  
 상태를 표시할 빈도(초)를 지정합니다.  
  
 **-f** 를 지정하지 않을 경우 기본 간격은 30초입니다.  
  
## <a name="examples"></a>예  
 이 예에서는 분산 재생 동작의 대부분이 수정된 재생 구성 파일인 `DReplay.exe.replay.config`에서 파생됩니다.  
  
-   **-m** 매개 변수는 `controller1` 이라는 컴퓨터가 컨트롤러로 사용되도록 지정합니다. 컨트롤러 서비스가 다른 컴퓨터에서 실행 중일 때는 컴퓨터 이름을 반드시 지정해야 합니다.  
  
-   **-d** 매개 변수는 컨트롤러에서 중간 파일의 위치( `c:\WorkingDir`)를 지정합니다.  
  
-   **-o** 매개 변수는 지정된 각 클라이언트가 재생 작업을 캡처하여 결과 추적 파일에 저장하도록 지정합니다. 참고: 구성 파일의 `<ResultTrace>` 요소를 사용하면 행 개수 및 결과 집합을 기록할지 여부를 지정할 수 있습니다.  
  
-   **-w** 매개 변수는 `client1` 부터 `client4` 까지의 컴퓨터가 분산 재생에 클라이언트로 참여하도록 지정합니다.  
  
-   **-c** 매개 변수는 수정된 구성 파일인 `DReplay.exe.replay.config`를 가리키는 데 사용됩니다.  
  
-   재생 구성 파일 **의** 요소에 `<Server>` 요소가 지정되어 있으므로 `<ReplayOptions>` -s `DReplay.exe.replay.config`매개 변수를 지정할 필요가 없습니다.  
  
 다음 구문을 사용하여 이벤트 재생 단계가 시작되며 이때 관리 도구는 컨트롤러와는 다른 컴퓨터에서 실행됩니다.  
  
```  
dreplay replay -m controller1 -d c:\WorkingDir -o -w client1,client2,client3,client4 -c c:\DReplay.exe.replay.config  
```  
  
 동기 시퀀스 모드를 지정하기 위해 `<SequencingMode>` 파일의 `DReplay.exe.replay.config` 요소가 `synchronization`값으로 설정되었습니다. 행 개수를 기록하도록 지정하기 위해 재생 구성 파일의 `<ResultTrace>` 섹션이 수정되었습니다. 다음 XML 예에서는 이러한 변경 내용을 보여 줍니다.  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance</Server>  
        <SequencingMode>synchronization</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
 스트레스 시퀀스 모드를 지정하기 위해 `<SequencingMode>` 파일의 `DReplay.exe.replay.config` 요소가 `stress`값으로 설정되었습니다. `<ConnectTimeScale>` 과 `<ThinkTimeScale>` 요소는 50%를 지정하기 위해 `50` 으로 설정되었습니다. 연결 시간 및 대기 시간에 대한 자세한 내용은 [Configure Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)를 참조하십시오. 다음 XML 예에서는 이러한 변경 내용을 보여 줍니다.  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server>server_name\replay_target_instance_name</Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale>50</ConnectTimeScale>  
        <ThinkTimeScale>50</ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="permissions"></a>사용 권한  
 관리 도구는 로컬 사용자 또는 도메인 사용자 등의 대화형 사용자 계정으로 실행해야 합니다. 로컬 사용자 계정을 사용하려면 관리 도구와 컨트롤러가 동일한 컴퓨터에서 실행되고 있어야 합니다.  
  
 자세한 내용은 [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [추적 데이터 재생](../../tools/distributed-replay/replay-trace-data.md)   
 [재생 결과 검토](../../tools/distributed-replay/review-the-replay-results.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed Replay 구성](../../tools/distributed-replay/configure-distributed-replay.md)   
 [SQL Server Distributed Replay 포럼](http://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Distributed Replay를 사용하여 SQL Server 테스트 로드 – 2단계](http://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Distributed Replay를 사용하여 SQL Server 테스트 로드 - 1단계](http://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
