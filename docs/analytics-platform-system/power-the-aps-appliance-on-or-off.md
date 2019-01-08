---
title: 전원을 켜거나-분석 플랫폼 시스템 어플라이언스 | Microsoft Docs
description: Analytics Platform System에 대 한 어플라이언스를 끄거나 전원
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 994b0f94448b7fb7901734b2ae737e26be23900f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527859"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Analytics Platform System에 대 한 어플라이언스를 끄거나 전원
이 항목에서는 어떻게 전원에 Analytics 플랫폼 Systemappliance 해제 전원 켜 짐 또는 실행 하 병렬 데이터 웨어하우스를 설명 합니다. 사용 하 여이 항목에서는 분석 플랫폼 시스템 어플라이언스를 이동 하면 하거나 전원 어플라이언스에서 심각한 전원 오류가 발생 한 후입니다.  
  
켜고 기기를 강화 되지 어플라이언스 서비스 시작 및 중지와 동일 합니다. 해당 주제에 대 한 자세한 내용은 [PDW 서비스 상태 &#40;Analytics Platform System&#41;](pdw-services-status.md)합니다. 전원을 켜거나 SQL Server 2008 Parallel Data Warehouse에 대 한 내용은 SQL Server 2008 병렬 데이터 웨어하우스 도움말 파일을 참조 하세요. 전원을 켜거나 AU2 병렬 데이터 웨어하우스 또는 SQL Server 2012 AU1을 해제 하는 방법에 대 한 내용은 해당 버전에 대 한 도움말 파일을 참조 하세요.  
  
연결이 연결 된 장치 (KVM)를 사용 하 여 로컬 수 있는 이러한 지침은 SQL Server PDW 노드에 연결 하기를 지정 하는 경우 또는 원격 데스크톱을 사용 하 여 원격입니다. 일부 동작은 (전원 스위치)를 설정 하는 물리적 컴퓨터 및 일부 (예: 종료) 있어야 합니다. Windows를 사용 하 여 명령 또는 물리적 일 수 있습니다.  
  
또는 노드에 할당 된 IP 주소를 사용 하 여 SQL Server PDW 노드에 연결을 만들 수 있습니다 합니다 **HST01** 중 하나를 사용 하 여 컴퓨터를 **장애 조치 클러스터 관리자** (**cluadmin.msc**) 또는 **Hyper-v 관리자** (**virtmgmt.msc**) 응용 프로그램 및 노드 이름을 마우스 오른쪽 단추로 클릭 합니다.  
  
## <a name="PowerOff"></a>어플라이언스를 끄지  
  
### <a name="before-you-begin"></a>시작하기 전 주의 사항  
어플라이언스 강화, 전에 어플라이언스에 대 한 모든 작업을 종료 해야 합니다. 모든 작업을 종료 합니다.  
  
-   사용 된 **세션** 현재 사용자를 식별 하는 관리자 콘솔의 페이지입니다. 연락 하 고 로그 오프를 요청 합니다.  
  
-   필요한 사용할 수 있습니다는 **KILL** 강제 클라이언트 연결을 종료 하는 문입니다. 종료 하는 경우 주의 사용 하 여 연결 합니다. 장기 실행 업데이트와 같은 트랜잭션 일부 프로세스를 중단 하는 경우 SQL Server 이전 롤백 활동 수 완료 해야 데이터베이스의 복구 합니다. 롤백하는 부분적으로 완료 된 업데이트 또는 삭제, 시간이 오래 걸릴 수 있습니다.  
  
### <a name="to-power-off-the-appliance"></a>어플라이언스를 끄지  
  
> [!WARNING]  
> 나열 된 정확한 순서로 모든 단계를 수행 해야 하 고 다른 설명이 없는 한 각 단계는 다음 단계를 수행 하기 전에 완료 해야 합니다. 잘못 된 순서 없이 각 단계가 완료 되기를 기다리는 단계를 수행 나중에 어플라이언스 전원이 켜진 경우 오류가 발생할 수 있습니다.  
  
1.  PDW 제어 노드에 연결 (**_PDW_region_-CTL01** ) 및 Analytics Platform System appliance 도메인 관리자 계정으로 로그인 합니다.  
  
2.  실행할 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` 열려면 합니다 **Configuration Manager**합니다.  
  
3.  Configuration Manager에서 아래를 **병렬 데이터 웨어하우스 토폴로지** 메뉴에서 클릭 합니다 **서비스 상태** 탭을 클릭 **중지 지역** PDW 서비스를 중지 하 합니다.   
  
4.  연결할  **_appliance_domain_-HST01** 어플라이언스 도메인 관리자 계정으로 로그인 합니다.  
  
5.  사용 하 여 합니다 **장애 조치 클러스터 관리자** 에 연결 합니다  **_appliance_domain_-WFOHST01** 자동으로 연결 하는 경우 클러스터 및 탐색 창에서 클릭 **역할**입니다. 에 **역할** 창:  
  
    1.  가상 머신의 모든 다중 선택 합니다. 마우스 오른쪽 단추로 클릭 **종료**합니다.  
  
    2.  모든 선택한 Vm 종료 하 고 완료 될 때까지 기다립니다.  
  
6.  닫기 합니다 **장애 조치 클러스터 관리자** 응용 프로그램입니다.  
  
7. 제외한 모든 서버를 종료할  **_appliance_domain_-HST01**합니다.  
  
8. 종료 합니다  **_appliance_domain_-HST01** 서버.  
  
9. 전력 분배 장치 (Pdu)를 종료 합니다.  
  
## <a name="PowerOn"></a>어플라이언스에서 전원  
  
### <a name="to-power-on-the-appliance"></a>어플라이언스 전원을  
  
> [!WARNING]  
> 나열 된 정확한 순서로 모든 단계를 수행 해야 하 고 다른 설명이 없는 한 각 단계는 다음 단계를 수행 하기 전에 완료 해야 합니다. 순서 없이 각 단계가 완료 되기를 기다리는 단계 시작 오류가 발생할 수 있습니다.  
  
1.  전력 분배 장치 (PDU의) 및 스위치에 대 한 대기를 자동으로 시작의 전원을 켭니다.  
  
2.  전원 켜기 합니다  **_appliance_domain_-HST01** 서버.  
  
3.  에 로그인  **_appliance_domain_-HST01** 어플라이언스 도메인 관리자 권한으로 합니다.  
  
4.  시작 합니다 **Hyper-v 관리자** 프로그램 (**virtmgmt.msc**)에 연결한  **_appliance_domain_-HST01** 기본적으로 연결 되지 않은 경우.  
  
    1.  때문에 이름으로 연결할 수 없는 경우는  **_PDW_region_-AD01** 는 실행 되지 않는 IP 주소를 사용 하 여 연결 시도 합니다.  
  
    2.  에 **Virtual Machines** 창 찾습니다  **_PDW_region_-AD01** 하 고 실행 중인지 확인 합니다. 그렇지 않은 경우이 VM을 시작 하 고 완전히 시작 되려면 일 기다립니다.  
  
5.  어플라이언스에서 서버의 나머지의 전원을 켭니다.  
  
6.  에 있는 동안 **HST01** 에서 어플라이언스 도메인 관리자로 로그온 **Hyper-v 관리자**:  
  
    1.  연결할  **_appliance_domain_-HST02**합니다.  
  
    2.  에 **Virtual Machines** 창 찾습니다  **_PDW_region_-AD02** 하 고 실행 중인지 확인 합니다.  그렇지 않은 경우이 VM을 시작 하 고 완전히 시작 되려면 일 기다립니다.  
  
7.  사용 하 여는 **장애 조치 클러스터 관리자** 에 연결 합니다  **_appliance_domain_-WFOHST01** 클러스터를 자동으로 연결 하는 경우 선택한 다음는  **탐색** 창 클릭 **역할**입니다. 에 **역할** 창:  
  
    1.  다중 선택의 모든 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 **시작**합니다.  
  
    2.  선택한 모든 Vm이 다음 단계를 진행 하기 전에 시작이 완료 될 때까지 기다립니다.  
  
    3.  장애 조치 Vm에 대 한 필요한 경우 종료할 이동할 및 적절 한 기본 호스트에서 다시 시작 합니다.  
  
8. 연결 끊기 **HST01** 하려는 경우.  
  
9. 연결할  **_PDW_region_-CTL01** 어플라이언스 도메인 관리자 계정을 사용 합니다.  
  
10. 실행 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` 를 시작 합니다 **Configuration Manager**합니다.  
  
11. 에 **Configuration Manager**를 **병렬 데이터 웨어하우스 토폴로지** 메뉴에서 클릭는 **서비스 상태** 탭을 클릭 **시작 지역**PDW 서비스를 시작 합니다.  
  
### <a name="to-verify-the-appliance-health"></a>어플라이언스 상태를 확인 하려면  
어플라이언스 시작 된 후 엽니다는 **관리 콘솔** 오류 상태를 나타낼 수 있는 경고에 대 한 상태 페이지를 확인 합니다. 자세한 내용은 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[어플라이언스 관리 작업 &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
