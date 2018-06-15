---
title: Configuration Manager-분석 플랫폼 시스템 시작 | Microsoft Docs
description: 분석 플랫폼 시스템 어플라이언스에 대 한 구성 관리자 도구를 시작 하기 위한 지침입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2e7a726386aa64d04f87f30cd22328900b1e5cd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544785"
---
# <a name="launch-the-configuration-manager-in-analytics-platform-system"></a>분석 플랫폼 시스템에서 구성 관리자를 시작 합니다.
시작 하기 위한 지침을 제공 하는이 항목의 **Configuration Manager** 분석 플랫폼 시스템 어플라이언스에 대 한 합니다.  
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="prerequisites"></a>필수 구성 요소  
분석 플랫폼 시스템**Configuration Manager** 기기 도메인 관리자만 실행할 수 있습니다. 이 도구를 실행 하려면 기기 도메인 관리자에 대 한 암호가 필요 합니다. 참조 추가 APS 관리자 만들려고 [프로그램 APS 도메인 관리자를 만듭니다 &#40;APS&#41;](create-an-aps-domain-administrator-aps.md)합니다.  
  
## <a name="Accessing"></a>구성 관리자 도구를 시작 합니다.  
구성 관리자를 실행 하려면 원격 데스크톱을 사용 하는 PDW 제어 노드에 연결 (***PDW_region *-CTL01**) 노드를 및로 로그인 * appliance_domain ***\Administrator**합니다. 시작할 때의 **Configuration Manager** 프로그램에서 사용 하 여는 **관리자 권한으로 실행** 옵션을 관리자 자격 증명이 사용 됩니다.  
  
#### <a name="to-launch-from-a-browser-window"></a>브라우저 창에서를 시작 하려면  
  
1.  브라우저를 열고 디렉터리로 이동 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`합니다.  
  
2.  마우스 오른쪽 단추로 클릭 `dwconfig.exe` 클릭 하 고 **관리자 권한으로 실행**합니다.  
  
#### <a name="to-launch-from-a-command-prompt"></a>명령 프롬프트에서 시작 하려면  
  
1.  바탕 화면을 열고는 **시작** 메뉴에서 클릭 **프로그램**, 클릭 **Accessories**, 마우스 오른쪽 단추로 클릭 **명령 프롬프트** 를클릭한다음 **관리자 권한으로 실행**합니다.  
  
2.  명령 프롬프트에서 디렉터리를 변경 하려면 다음 명령을 입력: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`합니다.  
  
3.  명령 프롬프트에서 다음을 입력 `dwconfig.exe`합니다.  
  
후의 **Configuration Manager** 은 시작 왼쪽된 창에 나열 된 모든 사용 가능한 기능과 표시 됩니다. 이 섹션의 나머지 부분에서는 도구에서 사용할 수 있는 각 작업을 실행 하는 방법을 설명 합니다.  
  
닫고 종료 **Configuration Manager**, 클릭 **종료** 모든 화면의 오른쪽 아래 모서리에 있습니다.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>관련 항목:  
[관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
