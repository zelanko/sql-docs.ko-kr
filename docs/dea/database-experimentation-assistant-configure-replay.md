---
title: SQL Server 업그레이드를 위한 재생 구성
description: 데이터베이스 실험 도우미에 대 한 Distributed Replay 구성
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
ms.openlocfilehash: ae7c3c2a987d9fb048c1c3fa494978626abce06a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76761537"
---
# <a name="configure-distributed-replay-for-database-experimentation-assistant"></a>데이터베이스 실험 도우미에 대 한 Distributed Replay 구성

DEA (데이터베이스 실험 도우미)는 SQL Server 설치의 Distributed Replay 도구를 사용 하 여 캡처된 추적을 업그레이드 된 테스트 환경에 대해 재생 합니다. 올바른 쿼리 재생을 위해 전체 재생을 수행 하기 전에 작은 추적 파일을 사용 하 여 테스트를 실행 하는 것이 좋습니다.

## <a name="distributed-replay-requirements"></a>Distributed Replay 요구 사항

- Distributed Replay 컨트롤러 컴퓨터에서 IRF 파일을 만들려면 하드 드라이브 공간의 78%가 추가로 필요 합니다.
- 200 MB 또는 512 MB는 프로덕션 또는 성능 추적을 캡처하는 데 사용할 이상적인 추적 롤오버 크기입니다.
- Distributed Replay 컨트롤러 및 클라이언트 컴퓨터에 대 한 최소 CPU 및 RAM 요구 사항은 3.5 GB RAM의 단일 코어 CPU입니다.
- 하나의 컨트롤러와 4 개의 자식 컴퓨터가 프로덕션 추적을 재생 하는 데 사용 되기 때문에 재생 시간은 캡처 시간 보다 약 1.55 배 더 걸립니다.
- "게시 된" 버전의 프로덕션 및 성능 추적 정의 파일을 사용 하 고 성능 추적 정의를 사용 하 여 한 데이터베이스에 대 한 추적을 필터링 하는 경우 분석은 **성능 추적** 크기가 **프로덕션 추적** 크기 보다 약 15 배 더 크다는 것을 보여 줍니다.

## <a name="set-up-a-virtual-network-or-domain"></a>가상 네트워크 또는 도메인 설정

Distributed Replay 컴퓨터 간에 공통 계정을 사용 해야 합니다. 이 요구 사항 때문에 보안상의 이유로 가상 네트워크 또는 도메인 제어 네트워크에서 Distributed Replay를 실행 하는 것이 좋습니다.

- 환경에 컨트롤러 및 클라이언트 컴퓨터를 만듭니다.
- 컨트롤러와 클라이언트 컴퓨터가 네트워크를 통해 서로 ping 할 수 있는지 확인 합니다.
- Distributed Replay 클라이언트 컴퓨터는 SQL Server를 실행 하는 재생 대상 컴퓨터에 연결 되어 있어야 합니다.

## <a name="set-up-the-controller-service"></a>컨트롤러 서비스 설정

컨트롤러 서비스를 설정 하려면:

1. SQL Server 설치 관리자를 사용 하 여 Distributed Replay 컨트롤러를 설치 합니다. Distributed Replay 컨트롤러를 구성 하는 SQL Server 설치 관리자 마법사 단계를 건너뛴 경우 구성 파일을 통해 컨트롤러를 구성할 수 있습니다. 일반적인 설치에서 구성 파일은 C:\Program Files (x86) \Microsoft SQL Server\<version\>\Tools\DReplayController\DReplayController.config.에 있습니다.
2. Distributed Replay 컨트롤러 로그는 C:\Program Files (x86) \Microsoft SQL Server\<version\>\Tools\DReplayController\Log.에 있습니다.
3. Services.msc를 열고 **SQL Server Distributed Replay Controller** 서비스로 이동 합니다.
4. 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다. 서비스 계정을 네트워크의 컨트롤러 및 클라이언트 컴퓨터에 공통적인 계정으로 설정 합니다.
5. **확인** 을 선택 하 여 **속성** 창을 닫습니다.
6. Services.msc에서 **SQL Server Distributed Replay Controller** 서비스를 다시 시작 합니다. 명령줄에서 다음 명령을 실행 하 여 서비스를 다시 시작할 수도 있습니다.

   `NET STOP "SQL Server Distributed Replay Controller"`</br>
   `NET START "SQL Server Distributed Replay Controller"`

추가 구성 옵션은 [Configure Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)를 참조 하세요.

## <a name="configure-dcom"></a>DCOM 구성

이 구성은 컨트롤러 컴퓨터에만 필요 합니다.

1. Dcomcnfg.exe를 엽니다.
2. **구성 요소 서비스** > **컴퓨터** > **내 컴퓨터** > **DCOM 구성**을 확장 합니다.
3. **DCOM 구성**에서 **DReplayController**을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.
4. **보안** 탭을 선택합니다.
5. **시작 및 활성화 권한**에서 **사용자 지정**을 선택 하 고 **편집**을 선택 합니다.
6. 재생을 시작할 사용자를 추가 합니다. 사용자 로컬 시작 및 로컬 활성화 권한을 부여 합니다. 사용자가 원격으로 시작 하거나 활성화할 계획인 경우 사용자 원격 시작 및 원격 활성화 권한을 부여 합니다.
7. **확인** 을 선택 하 여 변경 내용을 커밋하고 **보안** 탭으로 돌아갑니다.
8. **액세스 권한**에서 **사용자 지정**을 선택 하 고 **편집**을 선택 합니다.
9. 재생을 시작할 사용자를 추가 합니다. 사용자에 게 로컬 액세스 권한을 부여 합니다. 사용자가 컨트롤러 서비스에 원격으로 액세스 하려는 경우 사용자에 게 원격 액세스 권한을 제공 합니다.
10. **확인** 을 선택 하 여 변경 내용을 커밋하고 **보안** 탭으로 돌아갑니다.
11. **확인** 을 선택 하 여 변경 내용을 커밋합니다.
12. Services.msc에서 SQL Server Distributed Replay Controller 서비스를 다시 시작 합니다. 명령줄에서 다음 명령을 실행 하 여 서비스를 다시 시작할 수도 있습니다.

    `NET STOP "SQL Server Distributed Replay Controller"`</br>
    `NET START "SQL Server Distributed Replay Controller"`

## <a name="set-up-the-client-service"></a>클라이언트 서비스 설정

클라이언트 서비스를 설정 하기 전에 ping과 같은 네트워킹 도구를 사용 하 여 컨트롤러 및 클라이언트 컴퓨터가 통신할 수 있는지 확인 합니다.

1. SQL Server 설치 관리자를 사용 하 여 Distributed Replay 클라이언트를 설치 합니다.
2. Services.msc를 열고 SQL Server Distributed Replay 클라이언트 서비스로 이동 합니다.
3. 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다. 서비스 계정을 네트워크의 컨트롤러 및 클라이언트 컴퓨터에 공통 되는 계정으로 설정 합니다.
4. **확인** 을 선택 하 여 **속성** 창을 닫습니다. Distributed Replay 클라이언트를 구성 하는 SQL Server 설치 관리자 마법사 단계를 건너뛴 경우 구성 파일을 통해 구성할 수 있습니다. 일반적인 설치에서 구성 파일은 C:\Program Files (x86) \Microsoft SQL Server\<version\>\Tools\DReplayClient\DReplayClient.config.에 있습니다.
5. DReplayClient 파일에 컨트롤러 컴퓨터의 이름을 등록을 위한 컨트롤러로 포함 하는지 확인 합니다.
6. Services.msc에서 클라이언트 서비스 Distributed Replay SQL Server을 다시 시작 합니다. 명령줄에서 다음 명령을 실행 하 여 서비스를 다시 시작할 수도 있습니다.

    `NET STOP "SQL Server Distributed Replay Client"`</br>
    `NET START "SQL Server Distributed Replay Client"`

    Distributed Replay 컨트롤러 로그는 C:\Program Files (x86) \Microsoft SQL Server\<version\>\Tools\DReplayClient\Log.에 있습니다. 로그는 클라이언트가 컨트롤러에 자체 등록할 수 있는지 여부를 나타냅니다.

    구성에 성공 하면 컨트롤러 **<컨트롤러 이름\>에 등록**된 메시지가 로그에 표시 됩니다.

추가 구성 옵션은 [Configure Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/configure-distributed-replay)를 참조 하세요.

## <a name="set-up-distributed-replay-administration-tools"></a>Distributed Replay 관리 도구 설정

Distributed Replay 관리 도구를 사용 하 여 Distributed Replay 환경에서 제대로 작동 하는지 여부를 신속 하 게 테스트할 수 있습니다. 구성 테스트는 여러 클라이언트 컴퓨터를 컨트롤러에 등록 하는 환경에서 특히 유용할 수 있습니다. 관리 도구를 가져오려면 SSMS (SQL Server Management Studio)를 설치 해야 할 수 있습니다.

1. SSMS 설치 위치로 이동 하 여 Distributed Replay 관리 도구 dreplay와 종속 구성 요소를 찾습니다.
2. 명령 프롬프트에서를 실행 `dreplay.exe status -f 1`합니다.

위의 단계가 성공적으로 완료 되 면 콘솔 출력은 컨트롤러에서 `READY` 상태의 클라이언트를 볼 수 있음을 나타냅니다.

## <a name="configure-the-firewall-for-remote-distributed-replay-access"></a>원격 Distributed Replay 액세스에 대 한 방화벽 구성

Distributed Replay 원격으로 액세스 하려면 도메인 또는 가상 네트워크 내에 표시 되는 포트를 열어야 합니다.

1. **고급 보안이**포함 된 **Windows 방화벽** 을 엽니다.
2. **인바운드 규칙**으로 이동 합니다.
3. C:\Program Files (x86) \Microsoft SQL Server\<버전\>\Tools\DReplayController\DReplayController.exe. 프로그램에 대 한 새 인바운드 방화벽 규칙을 만듭니다.
4. DReplayController의 모든 포트에 대 한 도메인 수준 액세스에서 컨트롤러 서비스와 원격으로 통신할 수 있도록 허용 합니다.
5. 규칙을 저장합니다.

## <a name="set-up-target-computers"></a>대상 컴퓨터 설정

A/B 테스트 또는 실험을 실행 하려면 두 번 재생 해야 합니다. 즉, 마이그레이션 시나리오의 경우 두 개의 개별 SQL Server 설치 인스턴스가 필요할 수 있습니다.

동일한 컴퓨터에 두 가지 버전의 SQL Server 인스턴스를 설치할 수도 있습니다. 주의 사항은 재생이 진행 중일 때 인스턴스가 격리 되는지 확인 하는 것입니다.

각 재생에 대해 다음 단계를 수행 해야 합니다.

1. 데이터베이스의 백업을 복원 합니다.
2. 클라이언트 서비스 계정 사용자가 SQL Server 인스턴스의 데이터베이스에 액세스할 수 있는 권한을 제공 합니다. SQL Server 인스턴스에서 쿼리를 실행 하려면 권한이 필요 합니다.
3. 재생을 시작 합니다.

## <a name="see-also"></a>참고 항목

- 업그레이드 된 테스트 환경에서 캡처된 추적을 재생 하는 방법을 알아보려면 [데이터베이스 실험 도우미에서 추적 재생](database-experimentation-assistant-replay-trace.md)을 참조 하세요.
