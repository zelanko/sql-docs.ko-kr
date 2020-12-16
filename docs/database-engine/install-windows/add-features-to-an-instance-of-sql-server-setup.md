---
title: SQL Server 인스턴스에 기능 추가(설치 프로그램)
description: 이 문서에서는 SQL Server 2019 인스턴스에 인스턴스 인식 기능을 추가하기 위한 단계별 절차에 대해 설명합니다.
ms.prod: sql
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- feature adding [SQL Server]
- " SQL Server, features"
- adding features to  SQL Server
ms.assetid: 97931fdc-d943-48dd-81b9-ae8b8d2c6dad
author: cawrites
ms.author: chadam
ms.reviewer: ''
ms.custom: ''
ms.date: 09/07/2019
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 3481a3d5252752e1cf952375d1c35c1c4b9939f1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438836"
---
# <a name="add-features-to-an-instance-of-sql-server-setup"></a>SQL Server 인스턴스에 기능 추가(설치 프로그램)

[!INCLUDE [ SQL Server - Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

이 문서에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에 기능을 추가하기 위한 단계별 절차에 대해 설명합니다. 일부 SQL Server 구성 요소 또는 서비스는 SQL Server의 특정 인스턴스에 한정됩니다. 이를 인스턴스 인식 구성 요소 또는 서비스라고도 합니다. 인스턴스 인식 구성 요소 또는 서비스는 자신을 호스팅하는 인스턴스와 같은 버전을 공유하고 해당 인스턴스에만 독점적으로 사용됩니다. SQL Server 인스턴스에 공유 구성 요소(아직 설치되지 않은 경우)와 함께 인스턴스 인식 구성 요소를 추가할 수 있습니다. SQL Server 다른 버전에서 지원되는 기능 목록은 [SQL Server 2017의 버전 및 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.

명령 프롬프트에서 SQL Server 인스턴스에 기능을 추가하려면 [명령 프롬프트에서 SQL Server 설치](./install-sql-server-from-the-command-prompt.md)를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

계속하기 전에 [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md) 문서를 검토합니다.

> [!NOTE]
> 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유에서 SQL Server를 설치하는 경우 원격 공유에 대한 읽기 권한이 있는 도메인 계정을 사용해야 합니다.  
  
> [!NOTE]
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에 기능을 추가할 경우 기존 사용 보고서 설정이 새로 추가된 기능에 적용됩니다. 이러한 설정을 변경하려면 SQL Server의 **구성 도구** 메뉴에서 **SQL Server 오류 및 사용 보고** 도구를 사용합니다.

## <a name="procedures"></a>프로시저

#### <a name="to-add-features-to-an-instance-of-sscurrent"></a>명령 프롬프트에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]

1. SQL Server 설치 미디어를 넣습니다. 루트 폴더에서 setup.exe를 두 번 클릭합니다. 네트워크 공유에서 설치하려면 공유에서 루트 폴더로 이동한 다음 setup.exe를 두 번 클릭합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 대화 상자가 나타나면 **확인** 을 클릭하여 필수 구성 요소를 설치한 다음, **취소** 를 클릭하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치를 끝냅니다.  

2. 설치 마법사가 SQL Server 설치 센터를 시작합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 기존 인스턴스에 새 기능을 추가하려면 왼쪽 탐색 영역에서 **설치** 를 선택한 다음 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가** 를 클릭합니다.

3. 시스템 구성 검사기가 컴퓨터에서 검색 작업을 실행합니다. 확인 정보를 보려면 **자세히 보기** 를 선택합니다. 계속하려면 **확인** 을 선택합니다.

4. 제품 업데이트 페이지에는 사용 가능한 최신 SQL Server 제품 업데이트가 표시됩니다. 업데이트를 포함하지 않으려면 **SQL Server 제품 업데이트 포함** 확인란의 선택을 취소합니다. 제품 업데이트가 검색되지 않으면 SQL Server 설치 프로그램에서 이 페이지가 표시되지 않으며 **설치 파일 설치** 페이지로 자동으로 진행됩니다.

5. 설치 프로그램에서 설치 파일 설치 페이지에는 설치 파일의 다운로드, 추출 및 설치 진행률이 표시됩니다. SQL Server 설치 프로그램에 대한 업데이트가 발견되고 이러한 업데이트가 포함되도록 지정된 경우 해당 업데이트도 함께 설치됩니다. **설치** 를 선택하여 설치 지원 파일을 설치합니다.  

6. 시스템 구성 검사기는 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다.  

7. 설치 유형 페이지에서 **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 기존 인스턴스에 기능 추가** 옵션을 선택하고 업데이트하려는 인스턴스를 선택합니다.

8. 기능 선택 페이지에서 설치할 구성 요소를 선택합니다. 기능 이름을 선택하면 오른쪽 창에 각 구성 요소 그룹에 대한 설명이 나타납니다. 확인란을 자유롭게 조합하여 선택할 수 있습니다. 자세한 내용은 [SQL Server 2017의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요. 각 구성 요소는 해당 SQL Server 인스턴스에 한 번만 설치할 수 있습니다. 여러 구성 요소를 설치하려면 추가 SQL Server 인스턴스를 설치해야 합니다.

    선택한 기능의 필수 구성 요소가 오른쪽 창에 표시됩니다. 설치되어 있지 않은 필수 구성 요소가 있는 경우 SQL Server 설치 프로그램은 이 절차의 뒷부분에 설명된 설치 단계에서 이를 설치합니다.

    시스템 구성 검사기는 설치를 계속하기 전에 컴퓨터의 시스템 상태를 확인합니다. 계속하려면 **다음** 을 선택합니다.

9. 디스크 공간 요구 사항 페이지에서는 사용자가 지정한 기능에 필요한 디스크 공간을 계산하여 설치 프로그램을 실행하는 동안 컴퓨터에서 사용 가능한 디스크 공간과 이러한 요구 사항을 비교하여 보여 줍니다.

10. 이 문서의 나머지 부분에 대한 워크플로는 설치에 대해 지정한 기능에 따라 달라집니다. 선택 항목에 따라 일부 페이지가 표시되지 않을 수도 있습니다.

11. 서버 구성 - 서비스 계정 페이지에서 SQL Server 서비스에 대한 로그인 계정을 지정합니다. 이 페이지에 구성된 실제 서비스는 사용자가 설치하도록 선택한 기능에 따라 달라집니다.

    모든 SQL Server 서비스에 동일한 로그인 계정을 할당하거나 각 서비스 계정을 따로 구성할 수 있습니다. 서비스 시작 유형을 자동 또는 수동으로 지정하거나 서비스의 해제 여부도 지정할 수 있습니다. Microsoft는 서비스 계정을 개별적으로 구성하여 각 서비스에 대해 최소한의 권한만 제공할 것을 권장합니다. 이렇게 하면 SQL Server 서비스에서 작업을 완료하는 데 필요한 최소한의 권한만 부여할 수 있습니다. 자세한 내용은 [서버 구성 - 서비스 계정](./install-sql-server.md) 및 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

    이 SQL Server 인스턴스의 모든 서비스 계정에 대해 동일한 로그인 계정을 지정하려면 페이지 맨 아래에 있는 필드에 자격 증명을 제공합니다.

    **보안 정보** : [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]

    SQL Server 서비스에 대한 로그인 정보 지정을 완료하면 **다음** 을 클릭합니다.

12. 데이터베이스 엔진 및 Analysis Services에 기본이 아닌 데이터 정렬을 지정하려면 **서버 구성 - 데이터 정렬** 탭을 사용합니다. 자세한 내용은 [서버 구성 - 데이터 정렬](./install-sql-server.md)을 참조하세요.

13. 데이터베이스 엔진 구성 - 계정 프로비전 페이지를 사용하여 다음을 지정합니다.  

    - 보안 모드 - SQL Server 인스턴스에 대한 인증(Windows 인증 또는 혼합 모드 인증)을 선택합니다. 혼합 모드 인증을 선택하는 경우 기본 제공 SQL Server 시스템 관리자 계정에 강력한 암호를 제공해야 합니다.

        디바이스가 SQL Server에 성공적으로 연결되면 Windows 인증 및 혼합 모드에 모두 동일한 보안 메커니즘이 적용됩니다. 자세한 내용은 [데이터베이스 엔진 구성 - 서버 구성](./install-sql-server.md)을 참조하세요.  

    - SQL Server 관리자 지정 - SQL Server 인스턴스에 대해 시스템 관리자를 한 명 이상 지정해야 합니다. SQL Server 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가** 를 선택합니다. 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거** 를 선택한 다음, SQL Server 인스턴스의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다. 자세한 내용은 [데이터베이스 엔진 구성 - 서버 구성](./install-sql-server.md)을 참조하세요.

    목록 편집을 마쳤으면 **확인** 을 선택합니다. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록이 완료되면 **다음** 을 선택합니다.

14. 데이터베이스 엔진 구성 - 데이터 디렉터리 페이지를 사용하여 기본값이 아닌 설치 디렉터리를 지정할 수 있습니다. 기본 디렉터리에 설치하려면 **다음** 을 선택합니다.  

    > [!IMPORTANT]
    > 기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 SQL Server 인스턴스에 대해 고유한지 확인합니다. 이 대화 상자의 어떠한 디렉터리도 다른 SQL Server 인스턴스의 디렉터리와 공유되지 않아야 합니다.

    자세한 내용은 [데이터베이스 엔진 구성 - 데이터 디렉터리](./install-sql-server.md)를 참조하세요.

15. 데이터베이스 엔진 구성 - FILESTREAM 페이지를 사용하여 SQL Server 인스턴스에 대해 FILESTREAM을 사용하도록 설정할 수 있습니다. FILESTREAM에 대한 자세한 내용은 [데이터베이스 엔진 구성 - Filestream](./install-sql-server.md)을 참조하세요. 계속하려면 다음을 선택합니다.

16. Analysis Services 구성 - 계정 프로비저닝 페이지를 사용하여 서버 모드와 Analysis Services의 관리자 권한을 얻을 사용자 또는 계정을 지정할 수 있습니다. 서버 모드에 따라 해당 서버에서 사용되는 메모리 및 스토리지 하위 시스템이 결정됩니다. 각 솔루션 유형은 서로 다른 서버 모드로 실행됩니다. 서버에서 다차원 큐브 데이터베이스를 실행하려면 기본 옵션인 다차원 및 데이터 마이닝 서버 모드를 선택합니다. 관리자 권한의 경우 Analysis Services에 대해 시스템 관리자를 한 명 이상 지정해야 합니다. SQL Server 설치 프로그램을 실행 중인 계정을 추가하려면 **현재 사용자 추가** 를 선택합니다. 시스템 관리자 목록에서 계정을 추가하거나 제거하려면 **추가** 또는 **제거** 를 선택한 다음, Analysis Services 인스턴스의 관리자 권한이 있는 사용자, 그룹 또는 컴퓨터 목록을 편집합니다. 서버 모드 및 관리자 권한에 대한 자세한 내용은 [Analysis Services 구성 - 계정 프로비전](./install-sql-server.md)을 참조하세요.

    목록 편집을 마쳤으면 **확인** 을 선택합니다. 구성 대화 상자에서 관리자 목록을 확인합니다. 목록이 완료되면 **다음** 을 선택합니다.

17. Analysis Services 구성 - 데이터 디렉터리 페이지를 사용하여 기본값이 아닌 설치 디렉터리를 지정할 수 있습니다. 기본 디렉터리에 설치하려면 **다음** 을 선택합니다.

    > [!IMPORTANT]
    > 기본이 아닌 설치 디렉터리를 지정하는 경우 설치 폴더가 이 SQL Server 인스턴스에 대해 고유한지 확인합니다. 이 대화 상자의 어떠한 디렉터리도 다른 SQL Server 인스턴스의 디렉터리와 공유되지 않아야 합니다.

    자세한 내용은 [Analysis Services 구성 - 데이터 디렉터리](./install-sql-server.md)를 참조하세요.

18. Reporting Services 구성 페이지를 사용하여 만들 Reporting Services 설치 유형을 지정할 수 있습니다. Reporting Services 구성 모드에 대한 자세한 내용은 [Reporting Services 구성 옵션 &#40;SSRS&#41;](./install-sql-server.md)을 참조하세요.

19. Distributed Replay Controller 구성 페이지를 사용하여 Distributed Replay Controller 서비스에 대한 관리 권한을 부여할 사용자를 지정합니다. 관리 권한이 있는 사용자는 Distributed Replay Controller 서비스에 무제한으로 액세스할 수 있습니다.

    Distributed Replay Controller 서비스에 대한 액세스 권한을 부여할 사용자를 추가하려면 **현재 사용자 추가** 단추를 선택합니다. Distributed Replay Controller 서비스에 대한 액세스 권한을 추가하려면 **추가** 단추를 선택합니다. Distributed Replay Controller 서비스에서 액세스 권한을 제거하려면 **제거** 단추를 선택합니다.

    계속하려면 **다음** 을 선택합니다.

20. Distributed Replay Client 구성 페이지를 사용하여 Distributed Replay Client 서비스에 대한 관리 권한을 부여할 사용자를 지정합니다. 관리 권한이 있는 사용자는 Distributed Replay Client 서비스에 무제한으로 액세스할 수 있습니다.

    **컨트롤러 이름** 은 선택적 매개 변수이며 기본값은 \<*blank*>입니다. 클라이언트 컴퓨터에서 Distributed Replay Client 서비스를 위해 통신할 컨트롤러의 이름을 입력합니다. 다음 사항에 유의하세요.

    - 컨트롤러를 이미 설정한 경우 각 클라이언트를 구성할 때 컨트롤러의 이름을 입력합니다.

    - 컨트롤러를 아직 설정하지 않은 경우에는 컨트롤러 이름을 비워 둡니다. 그러나 **클라이언트 구성** 파일에서 컨트롤러 이름을 수동으로 입력해야 합니다.

    Distributed Replay Client 서비스의 **작업 디렉터리** 를 지정합니다. 기본 작업 디렉터리는 \<*drive letter*>:\Program Files\Microsoft\SQL Server\DReplayClient\WorkingDir입니다.

    Distributed Replay Client 서비스의 **결과 디렉터리** 를 지정합니다. 기본 결과 디렉터리는 \<*drive letter*>:\Program Files\Microsoft\SQL Server\DReplayClient\ResultDir입니다.

    계속하려면 **다음** 을 선택합니다.

21. 오류 보고 페이지에서 SQL Server 개선을 위해 Microsoft에 보내려는 정보를 지정합니다. 오류 보고 옵션은 기본적으로 사용됩니다.

22. 시스템 구성 검사기는 사용자가 지정한 SQL Server 기능에 따라 사용자 컴퓨터 구성의 유효성을 검사하기 위해 하나 이상의 규칙 집합을 실행합니다.  

23. 설치 준비 완료 페이지에는 설치 중에 지정된 설치 옵션이 트리 뷰로 표시됩니다. 설치 프로그램의 이 페이지에서는 제품 업데이트 기능이 사용하도록 설정되었는지 여부와 최종 업데이트 버전이 표시됩니다. 설치를 선택하면 SQL Server 설치 프로그램이 선택한 기능에 대한 필수 구성 요소를 먼저 설치하고 그 다음에 기능을 설치합니다.  

24. 설치 중에 설치 진행률 페이지에서 제공하는 상태 정보를 통해 설치 진행률을 모니터링할 수 있습니다.  

25. 설치가 끝나면 설치 및 기타 중요한 참고 사항에 대한 요약 로그 파일을 볼 수 있는 링크가 완료 페이지에 제공됩니다. SQL Server 설치 프로세스를 완료하려면 **닫기** 를 선택합니다.

26. 컴퓨터를 다시 시작합니다. 설치가 완료되면 설치 마법사에 표시되는 메시지를 꼭 읽으십시오. 설치 로그 파일에 대한 자세한 내용은 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

사용자 SQL Server 설치 구성

- SQL Server는 공격받을 수 있는 시스템의 노출 영역을 줄이기 위해 핵심 서비스와 기능을 선별하여 설치하고 활성화합니다. 자세한 내용은 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
- [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [SQL Server 설치 유효성 검사](../../database-engine/install-windows/validate-a-sql-server-installation.md)
- [실패한 SQL Server 2016 설치 복구](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)
- [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)
- [명령 프롬프트에서 SQL Server 설치](./install-sql-server-from-the-command-prompt.md)
