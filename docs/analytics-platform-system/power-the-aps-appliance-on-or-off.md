---
title: 어플라이언스 켜기 또는 끄기
description: 분석 플랫폼 시스템에 대해 어플라이언스 기능 설정 또는 해제
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee70338b5a46ec60d808e489d982fd80692c5d1d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400628"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대해 어플라이언스 기능 설정 또는 해제
이 항목에서는 병렬 데이터 웨어하우스를 실행 하는 Analytics Platform Systemappliance를 켜고 끄는 방법에 대해 설명 합니다. 분석 플랫폼 시스템 어플라이언스를 이동 하거나 치명적인 전원 오류가 발생 한 후 어플라이언스를 켤 때이 항목을 사용 합니다.  
  
어플라이언스를 켜고 끄는 것은 어플라이언스 서비스를 시작 및 중지 하는 것과 동일 하지 않습니다. 해당 주제에 대 한 자세한 내용은 [PDW 서비스 상태 &#40;분석 플랫폼 시스템&#41;](pdw-services-status.md)을 참조 하세요. SQL Server 2008 병렬 데이터 웨어하우스의 전원을 켜거나 끄는 방법에 대 한 자세한 내용은 SQL Server 2008 Parallel Data Warehouse 도움말 파일을 참조 하세요. SQL Server 2012 AU1 또는 AU2 Parallel 데이터 웨어하우스의 전원을 켜거나 끄는 방법에 대 한 자세한 내용은 해당 버전에 대 한 도움말 파일을 참조 하세요.  
  
이러한 지침이 SQL Server PDW 노드에 대 한 연결을 지정 하는 경우 연결 된 장치 (KVM)를 사용 하 여 로컬 또는 원격 데스크톱을 사용 하는 원격 연결을 사용할 수 있습니다. 일부 작업은 물리적 이어야 하 고 (전원 스위치를 켜는 경우) 일부 작업 (예: 종료)은 물리적 이거나 Windows 명령을 사용 하 여 수행할 수 있습니다.  
  
노드에 할당 된 IP 주소를 사용 하거나 **장애 조치(Failover) 클러스터 관리자** (**Cluadmin.msc**) 또는 **hyper-v 관리자** (**virtmgmt**) 응용 **HST01** 프로그램을 사용 하 여 노드 이름을 마우스 오른쪽 단추로 클릭 하 여 SQL Server PDW 노드에 대 한 연결을 설정할 수 있습니다.  
  
## <a name="power-off-the-appliance"></a><a name="PowerOff"></a>어플라이언스 전원 끄기  
  
### <a name="before-you-begin"></a>시작하기 전에  
어플라이언스의 전원을 끄기 전에 어플라이언스의 모든 작업을 종료 해야 합니다. 모든 작업을 종료 하려면:  
  
-   관리 콘솔의 **세션** 페이지를 사용 하 여 현재 사용자를 식별할 수 있습니다. 담당자에 게 연락 하 여 로그 오프 하도록 요청 하세요.  
  
-   필요한 경우 **KILL** 문을 사용 하 여 클라이언트 연결을 강제로 종료할 수 있습니다. 연결을 종료할 때는 주의 해야 합니다. 중단 된 경우 장기 실행 업데이트와 같은 일부 트랜잭션 프로세스는 데이터베이스의 복구를 완료할 수 SQL Server 하기 전에 작업을 롤백해야 합니다. 부분적으로 완료 된 업데이트 또는 삭제를 롤백하는 데 시간이 오래 걸릴 수 있습니다.  
  
### <a name="to-power-off-the-appliance"></a>어플라이언스의 전원을 끄려면  
  
> [!WARNING]  
> 모든 단계는 표시 된 순서 대로 수행 해야 하며, 별도로 명시 되지 않은 한, 다음 단계를 수행 하기 전에 각 단계를 완료 해야 합니다. 순서를 벗어난 단계를 수행 하거나 각 단계가 완료 될 때까지 기다리지 않고 단계를 수행 하면 나중에 어플라이언스를 켤 때 오류가 발생할 수 있습니다.  
  
1.  PDW 제어 노드**_PDW_region_(CTL01** )에 연결 하 고 분석 플랫폼 시스템 어플라이언스 도메인 관리자 계정으로 로그인 합니다.  
  
2.  `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`를 실행 하 여 **Configuration Manager**를 엽니다.  
  
3.  Configuration Manager의 **병렬 데이터 웨어하우스 토폴로지** 메뉴에서 **서비스 상태** 탭을 클릭 하 고 **중지 영역** 을 클릭 하 여 PDW 서비스를 중지 합니다.   
  
4.  ** _Appliance_domain_-HST01** 에 연결 하 고 어플라이언스 도메인 관리자 계정으로 로그인 합니다.  
  
5.  **장애 조치(Failover) 클러스터 관리자** 사용 하 여 자동으로 연결 되지 않은 경우 WFOHST01 클러스터 ** _appliance_domain_** 에 연결 하 고 탐색 창에서 **역할**을 클릭 합니다. **역할** 창에서 다음을 수행 합니다.  
  
    1.  모든 가상 컴퓨터를 다중 선택 합니다. 해당 항목을 마우스 오른쪽 단추로 클릭 하 고 **종료**를 선택 합니다.  
  
    2.  선택한 모든 Vm의 종료가 완료 될 때까지 기다립니다.  
  
6.  **장애 조치(Failover) 클러스터 관리자** 응용 프로그램을 닫습니다.  
  
7. ** _Appliance_domain_-HST01**를 제외한 모든 서버를 종료 합니다.  
  
8. ** _Appliance_domain_-HST01** 서버를 종료 합니다.  
  
9. Pdu (전원 분배 장치)를 종료 합니다.  
  
## <a name="power-on-the-appliance"></a><a name="PowerOn"></a>어플라이언스의 전원 켜기  
  
### <a name="to-power-on-the-appliance"></a>어플라이언스를 구동 하려면  
  
> [!WARNING]  
> 모든 단계는 표시 된 순서 대로 수행 해야 하며, 별도로 명시 되지 않은 한, 다음 단계를 수행 하기 전에 각 단계를 완료 해야 합니다. 순서를 벗어난 단계를 수행 하거나 각 단계가 완료 될 때까지 기다리지 않고 단계를 수행 하면 시작 오류가 발생할 수 있습니다.  
  
1.  PDU (전원 분배 장치)의 전원을 켜고 스위치가 자동으로 시작 될 때까지 기다립니다.  
  
2.  ** _Appliance_domain_HST01** 서버의 전원을 켭니다.  
  
3.  ** _Appliance_domain_-HST01** 에 로그인 하 여 어플라이언스 도메인 관리자로 로그인 합니다.  
  
4.  **Hyper-v 관리자** 프로그램 (**virtmgmt**)을 시작 하 고 기본적으로 연결 되어 있지 않으면 ** _appliance_domain_-HST01** 에 연결 합니다.  
  
    1.  ** _PDW_region_-AD01** 가 실행 되 고 있지 않으므로 이름으로 연결할 수 없는 경우 IP 주소를 사용 하 여 연결을 시도 합니다.  
  
    2.  **Virtual Machines** 창에서 ** _PDW_region_AD01** 를 찾아 실행 중인지 확인 합니다. 그렇지 않은 경우이 VM을 시작 하 고 완전히 시작 될 때까지 기다립니다.  
  
5.  기기의 나머지 서버 전원을 켭니다.  
  
6.  **Hyper-v 관리자**에서 어플라이언스 도메인 관리자로 로그온 한 **HST01** :  
  
    1.  ** _Appliance_domain_-HST02**에 연결 합니다.  
  
    2.  **Virtual Machines** 창에서 ** _PDW_region_AD02** 를 찾아 실행 중인지 확인 합니다.  그렇지 않은 경우이 VM을 시작 하 고 완전히 시작 될 때까지 기다립니다.  
  
7.  **장애 조치(Failover) 클러스터 관리자** 사용 하 여 자동으로 연결 되지 않은 경우 WFOHST01 클러스터 ** _appliance_domain_** 에 연결 하 고 **탐색** 창에서 **역할**을 클릭 합니다. **역할** 창에서 다음을 수행 합니다.  
  
    1.  모든 가상 컴퓨터를 다중 선택 하 고 마우스 오른쪽 단추로 클릭 한 다음 **시작**을 클릭 합니다.  
  
    2.  다음 단계로 진행 하기 전에 선택한 모든 Vm의 시작이 완료 될 때까지 기다립니다.  
  
    3.  장애 조치 (failover) 된 Vm에 대해 필요한 경우 해당 Vm을 종료 하 고 이동한 다음 적절 한 기본 호스트에서 다시 시작 합니다.  
  
8. 원하는 경우 **HST01** 에서 연결을 끊습니다.  
  
9. 어플라이언스 도메인 관리자 계정을 사용 하 여 ** _PDW_region_CTL01** 에 연결 합니다.  
  
10. `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`을 실행 하 여 **Configuration Manager**를 시작 합니다.  
  
11. **Configuration Manager**의 **병렬 데이터 웨어하우스 토폴로지** 메뉴에서 **서비스 상태** 탭을 클릭 하 고 **시작 영역** 을 클릭 하 여 PDW 서비스를 시작 합니다.  
  
### <a name="to-verify-the-appliance-health"></a>어플라이언스 상태를 확인 하려면  
기기가 시작 된 후 **관리 콘솔** 을 열고 상태 페이지에서 오류 상태를 나타낼 수 있는 경고를 확인 합니다. 자세한 내용은 [관리 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[기기 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
