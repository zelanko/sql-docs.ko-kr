---
title: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미에서 재생 구성
description: 데이터베이스 실험 도우미에서 재생 구성
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
ms.openlocfilehash: 9166265dad077d4a3e83cc300868607d001ef233
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058970"
---
# <a name="configure-replay-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 재생 구성

데이터베이스 실험 도우미 (비활성화)을 업그레이드 된 테스트 환경에 대해 캡처된 추적을 재생 하려면 SQL Server 설치에서 Distributed Replay 도구를 사용 합니다. 쿼리의 적절 한 재생 되도록 전체 재생을 수행 하기 전에 소규모 추적 파일을 사용 하 여 실행할 테스트를 수행 하는 것이 좋습니다.

## <a name="distributed-replay-requirements"></a>Distributed Replay 요구 사항

- 하드 드라이브 공간 추가 78% Distributed Replay 컨트롤러 컴퓨터에서 IRF 파일을 만드는 데 필요 합니다.
- 200MB 또는 512MB 프로덕션 또는 성능 추적을 캡처하는 데 이상적인 추적 롤오버 크기입니다.   
- Distributed Replay 컨트롤러 및 클라이언트 컴퓨터에 대 한 최소 CPU 및 RAM 요구 사항은 3.5GB RAM 사용 하 여 단일 코어 CPU입니다.
- 하나의 컨트롤러와 4 개의 자식 컴퓨터 프로덕션 추적 재생에 사용 되기 때문에 약 재생 시간 캡처 시간 보다 1.55 시간이 오래 걸립니다.
- 관심 하나의 데이터베이스에 대 한 생산 및 성능 추적 정의 파일 및 성능 추적 정의 필터링 추적의 "게시"이 버전을 사용 하는 경우 분석에 따르면 합니다 **성능 추적** 크기가 보다 약 15 배 큰 합니다 **프로덕션 추적** 크기입니다.

## <a name="set-up-a-virtual-network-or-domain"></a>가상 네트워크 또는 도메인 설정

Distributed Replay를 사용 하면 컴퓨터 간에 일반적인 계정을 사용 하도록 해야 합니다. 이 요구 사항으로 인해 및 보안상의 이유로 도메인 제어 네트워크 또는 가상 네트워크에서 Distributed Replay를 실행 하는 것이 좋습니다.

- 컨트롤러 및 클라이언트에서에서 컴퓨터를 만드는 환경입니다.
- 컨트롤러 및 클라이언트 컴퓨터에 ping 할 수 있는지 서로 네트워크를 통해 있는지 확인 합니다.
- Distributed Replay 클라이언트 컴퓨터에 SQL Server를 실행 하는 재생 대상 컴퓨터에 대 한 연결이 있어야 합니다.

## <a name="set-up-the-controller-service"></a>컨트롤러 서비스 설정

컨트롤러 서비스를 설정 하려면:

1. SQL Server 설치 관리자를 사용 하 여 Distributed Replay controller를 설치 합니다. Distributed Replay controller를 구성 하는 SQL Server 설치 관리자 마법사 단계를 건너뛴 경우에 구성 파일을 통해 컨트롤러를 구성할 수 있습니다. 일반적인 설치, 구성 파일의 위치를 가리키는 (x86) C:\Program Files \microsoft SQL Server\<버전\>\Tools\DReplayController\DReplayController.config 합니다.
1. C:\Program Files (x86) \microsoft SQL Server distributed Replay 컨트롤러 로그 위치한\<버전\>\Tools\DReplayController\Log 합니다.
1. Services.msc를 열고 다음으로 이동 합니다 **SQL Server Distributed Replay Controller** 서비스입니다.
1. 서비스를 마우스 오른쪽 단추로 클릭 하 고 선택한 **속성**합니다. 네트워크 컨트롤러 및 클라이언트 컴퓨터에 공통 된 계정에 서비스 계정을 설정 합니다.
1. 선택 **확인** 닫으려면 합니다 **속성** 창입니다.
1. 다시 시작 합니다 **SQL Server Distributed Replay Controller** Services.msc에서 서비스 합니다. 서비스를 다시 시작 하려면 명령줄에서 다음 명령을 실행할 수도 있습니다.<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`
1. 자세한 구성 옵션에 대해서 [Distributed Replay 구성](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)합니다.

## <a name="configure-dcom"></a>DCOM 구성

이 구성은 컨트롤러 컴퓨터에만 필요 합니다.

1. Dcomcnfg.exe를 엽니다.
1. 확장 **구성 요소 서비스** > **컴퓨터** > **컴퓨터로** > **DCOM 구성**합니다.
1. 아래 **DCOM 구성**를 마우스 오른쪽 단추로 클릭 **DReplayController**를 선택한 후 **속성**합니다.
1. **보안** 탭을 선택합니다.
1. 아래 **시작 및 활성화 권한**를 선택 **사용자 지정**를 선택한 후 **편집**합니다.
1. 재생을 시작할 수 있는 사용자를 추가 합니다. 로컬 실행 및 로컬 활성화 권한을 사용자에 게 제공 합니다. 사용자를 시작 하거나 원격으로 활성화할 경우, 원격 시작 및 원격 활성화 권한을 사용자에 게 제공 합니다.
1. 선택 **확인** 변경 내용을 커밋하고 반환 하는 **보안** 탭 합니다.
1. 아래 **액세스 권한을**를 선택 **사용자 지정**를 선택한 후 **편집**합니다.
1. 재생을 시작할 수 있는 사용자를 추가 합니다. 로컬 액세스 권한을 사용자에 게 제공 합니다. 컨트롤러 서비스를 원격으로 액세스 하려면 사용자 계획을 하는 경우 원격 액세스 권한을 사용자에 게 제공 합니다.
1. 선택 **확인** 변경 내용을 커밋하고 반환 하는 **보안** 탭 합니다.
1. 선택 **확인** 에 변경 내용을 커밋합니다.
1. Services.msc에서 SQL Server Distributed Replay Controller 서비스를 다시 시작 합니다. 서비스를 다시 시작 하려면 명령줄에서 다음 명령을 실행할 수도 있습니다.<br/>
   `NET STOP "SQL Server Distributed Replay Controller"`<br/>
   `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>클라이언트 서비스 설정

클라이언트 서비스를 설정 하기 전에 컨트롤러 및 클라이언트 컴퓨터에 통신할 수 있는지 확인 하려면 ping 같은 네트워킹 도구를 사용 합니다.

1. SQL Server 설치 관리자를 사용 하 여 Distributed Replay client를 설치 합니다.
1. Services.msc를 열고 SQL Server Distributed Replay Client 서비스를 이동 합니다.
1. 서비스를 마우스 오른쪽 단추로 클릭 하 고 선택한 **속성**합니다. 네트워크에서 컨트롤러 및 클라이언트 컴퓨터에 공통 되는 계정에 서비스 계정을 설정 합니다.
1. 선택 **확인** 닫으려면 합니다 **속성** 창입니다. Distributed Replay client를 구성 하는 SQL Server 설치 관리자 마법사 단계를 건너뛴 경우에 구성 파일을 통해 구성할 수 있습니다. 일반적인 설치, 구성 파일의 위치를 가리키는 (x86) C:\Program Files \microsoft SQL Server\<버전\>\Tools\DReplayClient\DReplayClient.config 합니다.
1. 등록에 대 한 해당 컨트롤러로 DReplayClient.config 파일에 컨트롤러 컴퓨터의 이름이 있는지 확인 합니다.
1.  Services.msc에서 SQL Server Distributed Replay Client 서비스를 다시 시작 합니다. 서비스를 다시 시작 하려면 명령줄에서 다음 명령을 실행할 수도 있습니다.<br/>
    `NET STOP "SQL Server Distributed Replay Client"`<br/>
    `NET START "SQL Server Distributed Replay Client"`
1. C:\Program Files (x86) \microsoft SQL Server distributed Replay 컨트롤러 로그 위치한\<버전\>\Tools\DReplayClient\Log 합니다. 로그 여부를 클라이언트 자체를 등록할 수는 컨트롤러를 나타냅니다.
1. 구성이 성공 하면 로그 메시지를 표시 하는 "컨트롤러에 등록 < 컨트롤러 이름\>"입니다.
1. 자세한 구성 옵션에 대해서 [Distributed Replay 구성](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)합니다.

## <a name="set-up-distributed-replay-administration-tools"></a>Distributed Replay 관리 도구 설정

Distributed Replay 환경에서 제대로 작동 하는지 여부를 빠르게 테스트 하기 위해 Distributed Replay 관리 도구를 사용할 수 있습니다. 구성을 테스트 하는 것은 컨트롤러를 사용 하 여 여러 클라이언트 컴퓨터를 등록 하는 환경에서 특히 유용할 수 있습니다. SQL Server Management Studio (SSMS)를 관리 도구를 설치 해야 합니다.

1. SSMS를 설치 위치를 찾아서 Distributed Replay 관리 도구 dreplay.exe 및 해당 종속 구성 요소를 이동 합니다.
1. 명령 프롬프트 창을 열고 실행 `dreplay.exe status -f 1`합니다.
1. 위의 모든 단계에 성공한 경우 콘솔 출력은 컨트롤러에서 해당 클라이언트를 볼 수 있는지를 나타냅니다는 `READY` 상태입니다.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>Distributed Replay에 대 한 원격 액세스에 대 한 방화벽 구성

Distributed Replay를 원격으로 액세스할 도메인 또는 가상 네트워크 내에서 표시 되는 포트 열기에 필요 합니다.

1. 오픈 **Windows 방화벽** 사용 하 여 **고급 보안**합니다.
1. 로 이동 **인바운드 규칙**합니다.
1. 프로그램 (x86) C:\Program Files \Microsoft SQL Server에 대 한 새 인바운드 방화벽 규칙을 만듭니다\<버전\>\Tools\DReplayController\DReplayController.exe 합니다.
1. 컨트롤러 서비스를 원격으로 통신할 수 있으려면 DReplayController.exe에 대 한 모든 포트에 대 한 도메인 수준 액세스를 허용 합니다.
1. 규칙을 저장 합니다.

## <a name="set-up-target-computers"></a>대상 컴퓨터 설정

두 재생 A를 실행 하는 데 필요한 / B 테스트 또는 실험 합니다. 즉, 마이그레이션 시나리오에 대 한 SQL Server 설치의 두 개별 인스턴스를 해야 할 수 있습니다. 

또한 동일한 컴퓨터에 두 버전의 SQL Server 인스턴스를 설치할 수 있습니다. 주의 해야 재생을 진행 중인 인스턴스가 완전히 격리 되어 있는지 확인 하는 것입니다.

각 재생을 위해 다음 단계를 수행 해야 합니다.

1. 데이터베이스의 백업을 복원 합니다.
1. SQL Server 인스턴스에서 데이터베이스에 액세스 하는 클라이언트 서비스 계정 사용자에 대 한 권한을 제공 합니다. 권한은 SQL Server 인스턴스에서 실행할 쿼리에 대 한 필요 합니다.
1. 재생을 시작 합니다.

## <a name="next-steps"></a>다음 단계

- 업그레이드 된 테스트 환경에서 캡처한 추적을 재생 하는 방법에 알아보려면 참조 [추적을 재생](database-experimentation-assistant-replay-trace.md)합니다.

- 비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
