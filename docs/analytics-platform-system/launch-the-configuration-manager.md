---
title: Analytics Platform System Configuration Manager-시작 | Microsoft Docs
description: Analytics Platform System 어플라이언스에 대 한 Configuration Manager 도구를 시작 하는 것에 대 한 지침입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 087360981a7c31de6980755cfee4f98f88f48a15
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502451"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>분석 플랫폼 시스템에 Configuration Manager 시작
이 항목에서는 시작 지침을 제공 합니다 **Configuration Manager** Analytics Platform System 어플라이언스에 대 한 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="prerequisites"></a>사전 요구 사항  
Analytics Platform System**Configuration Manager** 어플라이언스 도메인 관리자가 실행할 수 있습니다. 이 도구를 실행 하려면 어플라이언스 도메인 관리자에 대 한 암호가 필요 합니다. 참조 추가 AP 관리자를 만들려면 [APS 도메인 관리자를 만듭니다 &#40;AP&#41;](create-an-aps-domain-administrator-aps.md)합니다.  
  
## <a name="Accessing"></a>구성 관리자 도구를 시작 합니다.  
Configuration Manager를 실행 하려면 PDW 제어 노드에 연결 하려면 원격 데스크톱 사용 (**_PDW_region_-CTL01**) 노드와로 로그인 _appliance_domain_ **\Administrator**합니다. 시작할 때 합니다 **Configuration Manager** 프로그램에서 사용 하 여 합니다 **관리자 권한으로 실행** 관리자 자격 증명을 사용 하도록 옵션입니다.  
  
#### <a name="to-launch-from-a-browser-window"></a>브라우저 창에서 시작 하려면  
  
1.  브라우저를 열고 디렉터리를 이동할 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`합니다.  
  
2.  마우스 오른쪽 단추로 클릭 `dwconfig.exe` 을 클릭 한 다음 **관리자 권한으로 실행**합니다.  
  
#### <a name="to-launch-from-a-command-prompt"></a>명령 프롬프트에서 시작 하려면  
  
1.  바탕 화면에서 엽니다는 **시작** 메뉴에서 클릭 **프로그램**, 클릭 **Accessories**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트** 클릭및 **관리자 권한으로 실행**합니다.  
  
2.  명령 프롬프트에서 디렉터리를 변경 하려면 다음 명령을 입력: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`합니다.  
  
3.  명령 프롬프트에서 입력 `dwconfig.exe`합니다.  
  
후 합니다 **Configuration Manager** 는 시작 나타납니다 왼쪽된 창에 나열 된 사용 가능한 모든 기능입니다. 이 섹션의 나머지 부분에는 도구에서 사용할 수 있는 각 작업을 수행 하는 방법을 설명 합니다.  
  
닫고 종료 **Configuration Manager**, 클릭 **종료** 모든 화면의 오른쪽 아래 모퉁이에서.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>관련 항목:  
[관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
