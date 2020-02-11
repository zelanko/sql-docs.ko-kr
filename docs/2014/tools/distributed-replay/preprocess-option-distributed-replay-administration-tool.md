---
title: 전처리 옵션(Distributed Replay Utility Administration Tool) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 9b5012fd-233e-4a25-a2e1-585c63b70502
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f5f4492dc18a93ab1fea9d34287eb90703bc3d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63149911"
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>전처리 옵션(Distributed Replay Utility Administration Tool)
  Distributed Replay 관리 도구인 `DReplay.exe`는 Distributed Replay controller와 통신 하는 데 사용할 수 있는 명령줄 도구입니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이 항목에서는 **preprocess** 명령줄 옵션과 해당 구문에 대해 설명합니다.  
  
 
  **프로세스** 옵션은 전처리 단계를 시작합니다. 이 단계 동안 컨트롤러는 대상 서버에 대해 재생할 입력 추적 데이터를 준비합니다.  
  
 ![토픽 링크 아이콘](../../database-engine/media/topic-link.gif "항목 링크 아이콘") 관리 도구 구문과 함께 사용 되는 구문 표기 규칙에 대 한 자세한 내용은 transact-sql [구문 표기 규칙 &#40;transact-sql&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
      dreplay preprocess [-mcontroller] -iinput_trace_file  
    -dcontroller_working_dir [-cconfig_file] [-fstatus_interval]  
```  
  
#### <a name="parameters"></a>매개 변수  
 **-m** *컨트롤러*  
 컨트롤러의 컴퓨터 이름을 지정합니다. "`localhost`" 또는 "`.`"을 사용하여 로컬 컴퓨터를 참조할 수 있습니다.  
  
 
  **-m** 매개 변수를 지정하지 않으면 로컬 컴퓨터가 사용됩니다.  
  
 **-i** *input_trace_file*  
 컨트롤러에서 입력 추적 파일의 전체 경로(예: `D:\Mytrace.trc`)를 지정합니다. 
  **-i** 매개 변수는 필수 항목입니다.  
  
 같은 디렉터리에 롤오버 파일이 있으면 자동으로 로드되어 사용됩니다. 파일은 파일 롤오버 명명 규칙을 따라야 합니다(예: `Mytrace.trc`, `Mytrace_1.trc`, `Mytrace_2.trc`, `Mytrace_3.trc`, `Mytrace_n.trc`).  
  
> [!NOTE]  
>  컨트롤러와는 다른 컴퓨터에서 관리 도구를 사용하는 경우 이 매개 변수에 로컬 경로를 사용할 수 있도록 입력 추적 파일을 컨트롤러로 복사해야 합니다.  
  
 **-d** *controller_working_dir*  
 컨트롤러에서 중간 파일이 저장될 디렉터리를 지정합니다. 
  **-d** 매개 변수는 필수 항목입니다.  
  
 적용되는 요구 사항은 다음과 같습니다.  
  
-   디렉터리가 컨트롤러에 있어야 합니다.  
  
-   드라이브 문자로 시작하는 전체 경로(예: `c:\WorkingDir`)를 지정해야 합니다.  
  
-   경로가 백슬래시("`\`")로 끝나지 않아야 합니다.  
  
-   UNC 경로는 지원되지 않습니다.  
  
 **-c** *config_file*  
 전처리 구성 파일의 전체 경로이며, 다른 위치에 저장된 경우 전처리 구성 파일의 위치를 지정하는 데 사용됩니다. 이 매개 변수는 UNC 경로이거나 관리 도구를 실행하는 컴퓨터에 로컬로 있을 수 있습니다.  
  
 필터링이 필요 없거나 최대 유휴 시간을 수정하지 않으려는 경우에는 **-c** 매개 변수를 지정하지 않아도 됩니다.  
  
 
  **-c** 매개 변수를 지정하지 않을 경우 기본 전처리 구성 파일 `DReplay.exe.preprocess.config`가 사용됩니다.  
  
 **-f** *status_interval*  
 상태 메시지를 표시할 빈도(초)를 지정합니다.  
  
 
  **-f** 를 지정하지 않을 경우 기본 간격은 30초입니다.  
  
## <a name="examples"></a>예  
 이 예에서는 모든 기본 설정을 사용하여 전처리 단계가 시작됩니다. 
  `localhost` 값은 컨트롤러 서비스가 관리 도구와 동일한 컴퓨터에서 실행 중임을 나타냅니다. 
  *input_trace_file* 매개 변수는 입력 추적 데이터 `c:\mytrace.trc`의 위치를 지정합니다. 추적 파일 필터링은 사용되지 않으므로 **-c** 매개 변수는 지정할 필요가 없습니다.  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 이 예에서는 전처리 단계가 시작되고 수정한 전처리 구성 파일이 지정됩니다. 위의 예와는 달리 수정한 구성 파일을 다른 위치에 저장한 경우 **-c** 매개 변수를 사용하여 해당 위치를 가리켜야 합니다. 다음은 그 예입니다.  
  
```  
dreplay preprocess -m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 수정한 전처리 구성 파일에는 분산 재생 중 시스템 세션을 필터링하는 필터 조건이 추가되었습니다. 이 필터는 전처리 구성 파일 `<PreprocessModifiers>` 에서 `DReplay.exe.preprocess.config`요소를 수정하여 추가되었습니다.  
  
 다음은 수정된 구성 파일의 예입니다.  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>사용 권한  
 관리 도구는 로컬 사용자 또는 도메인 사용자 등의 대화형 사용자 계정으로 실행해야 합니다. 로컬 사용자 계정을 사용하려면 관리 도구와 컨트롤러가 동일한 컴퓨터에서 실행되고 있어야 합니다.  
  
 자세한 내용은 [Distributed Replay Security](distributed-replay-security.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [입력 추적 데이터 준비](prepare-the-input-trace-data.md)   
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Configure Distributed Replay](configure-distributed-replay.md)  
  
  
