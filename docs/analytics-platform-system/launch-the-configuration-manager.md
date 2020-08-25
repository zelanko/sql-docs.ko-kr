---
title: 시작 Configuration Manager
description: 분석 플랫폼 시스템 어플라이언스에 대 한 Configuration Manager 도구를 시작 하는 방법에 대 한 지침입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 421265abcf3731ed48ff34a6b199ba5cd3c6af5c
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74401050"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 Configuration Manager 시작
이 항목에서는 분석 플랫폼 시스템 어플라이언스에 대 한 **Configuration Manager** 를 시작 하기 위한 지침을 제공 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>사전 준비 사항  
분석 플랫폼 시스템**Configuration Manager** 는 어플라이언스 도메인 관리자만 실행할 수 있습니다. 이 도구를 실행 하려면 어플라이언스 도메인 관리자에 대 한 암호가 필요 합니다. 추가 AP 관리자를 만들려면 aps [도메인 관리자 &#40;ap&#41;만들기 ](create-an-aps-domain-administrator-aps.md)를 참조 하세요.  
  
## <a name="launch-the-configuration-manager-tool"></a><a name="Accessing"></a>Configuration Manager 도구 시작  
Configuration Manager를 실행 하려면 원격 데스크톱을 사용 하 여 PDW 컨트롤 노드 (**_PDW_region_-CTL01**) 노드에 연결 하 고 _appliance_domain_**\administrator**로 로그인 합니다. **Configuration Manager** 프로그램을 시작할 때 관리자 권한 **으로 실행** 옵션을 사용 하 여 관리자 자격 증명이 사용 되는지 확인 합니다.  
  
#### <a name="to-launch-from-a-browser-window"></a>브라우저 창에서 시작 하려면  
  
1.  브라우저를 열고 디렉터리로 이동 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 합니다.  
  
2.  를 마우스 오른쪽 단추로 클릭 한 `dwconfig.exe` 다음 **관리자 권한으로 실행**을 클릭 합니다.  
  
#### <a name="to-launch-from-a-command-prompt"></a>명령 프롬프트에서 시작 하려면  
  
1.  바탕 화면에서 **시작** 메뉴를 열고 **프로그램**, **보조 프로그램**을 차례로 클릭 하 고 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행**을 클릭 합니다.  
  
2.  명령 프롬프트에서 다음 명령을 입력 하 여 디렉터리를 변경 합니다. `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`  
  
3.  명령 프롬프트에서 `dwconfig.exe`을 입력합니다.  
  
**Configuration Manager** 시작 되 면 왼쪽 창에 나열 된 사용 가능한 모든 기능이 표시 됩니다. 이 섹션의 나머지 부분에서는 도구에서 사용 가능한 각 작업을 수행 하는 방법을 설명 합니다.  
  
**Configuration Manager**를 닫고 종료 하려면 화면의 오른쪽 아래에 있는 **끝내기** 를 클릭 합니다.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>참고 항목  
[관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
