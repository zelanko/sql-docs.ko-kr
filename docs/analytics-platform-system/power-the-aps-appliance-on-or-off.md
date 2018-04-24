---
title: 전원을 켜거나-분석 플랫폼 시스템 기기 | Microsoft Docs
description: 분석 플랫폼 시스템에 대 한 기기를 끄거나 전원
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 54829190d03a889ade31383662bf192516934012
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 기기를 끄거나 전원
이 항목에서는 전원을 켜거나 전원을 끄고 병렬 데이터 웨어하우스를 실행 하 고 필요에 따라 HDInsight 지역이 실행 하 여 분석 플랫폼 Systemappliance 하는 방법을 설명 합니다. 사용 하 여이 항목 분석 플랫폼 시스템 기기를 이동할 때 전원 기기에서 치명적인 정전 후.  
  
어플라이언스에 켜거나 전원을 켜는 중 않습니다 기기 서비스 시작 및 중지와 동일 합니다. 해당 주제에 대 한 자세한 내용은 참조 하십시오. [PDW 서비스 상태 &#40;분석 플랫폼 시스템&#41;](pdw-services-status.md)합니다. SQL Server 2008 병렬 데이터 웨어하우스를 켜거나 전원을 켜는 중에 대 한 내용은 SQL Server 2008 병렬 데이터 웨어하우스 도움말 파일을 참조 하십시오. 전원을 켜는 중 또는 SQL Server 2012 AU1 또는 AU2 병렬 데이터 웨어하우스를 해제 하는 방법에 대 한 내용은 해당 버전에 대 한 도움말 파일을 참조 하십시오.  
  
연결이 연결 된 장치 (KVM)를 사용 하 여 로컬 일 수 있습니다 이러한 지침은 SQL Server PDW 노드에 연결 하기를 지정 하는 경우 또는 원격 데스크톱을 사용 하 여 원격입니다. 일부 동작은 (전원 스위치)를 설정 하는 실제 메모리와 일부 (예: 종료) 있어야 합니다. 실제 수 하거나 Windows를 사용 하 여 명령입니다.  
  
또는 노드에 할당 된 IP 주소를 사용 하 여 SQL Server PDW 노드에 연결을 만들 수 있습니다는 **HST01** 중 하나를 사용 하 여 컴퓨터의 **장애 조치 클러스터 관리자** (**cluadmin.msc**) 또는 **Hyper-v 관리자** (**virtmgmt.msc**) 응용 프로그램 및 노드 이름을 마우스 오른쪽 단추로 클릭 합니다.  
  
## <a name="PowerOff"></a>전원 끄기 어플라이언스  
  
### <a name="before-you-begin"></a>시작하기 전 주의 사항  
전원 어플라이언스에 끄기, 하기 전에 어플라이언스에 대 한 모든 작업을 종료 해야 합니다. 모든 작업을 종료:  
  
-   사용 하 여 **세션** 현재 사용자를 식별 하는 관리자 콘솔의 페이지입니다. 연락 하 고 로그 오프 하도록 요청 합니다.  
  
-   필요한 사용할 수 있습니다는 **KILL** 문을 강제 클라이언트 연결을 종료 합니다. 중지 하면 때는 주의 연결 합니다. 장기 실행 업데이트와 같은 일부 트랜잭션 프로세스를 중단 해야 롤백 활동 전 SQL Server 완료할 수 있습니다는 데이터베이스의 복구. 롤백하는 부분적으로 완료 된 업데이트 또는 삭제, 시간이 많이 걸릴 수 있습니다.  
  
### <a name="to-power-off-the-appliance"></a>어플라이언스를 끄지  
  
> [!WARNING]  
> 나열 된 정확한 순서로 모든 단계를 수행 해야 하 고 다른 설명이 없는 각 단계는 다음 단계를 수행 하기 전에 완료 해야 합니다. 잘못 된 순서로 또는 각 단계를 완료 될 때까지 기다리지 않고 단계를 수행 어플라이언스에 나중에 전원을 경우 오류가 발생할 수 있습니다.  
  
1.  PDW 제어 노드에 연결 (***PDW_region *-CTL01** ) 분석 플랫폼 시스템 기기 도메인 관리자 계정 사용 하 여 로그인 합니다.  
  
2.  실행 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` 열려는 **Configuration Manager**합니다.  
  
3.  Configuration Manager에서 아래는 **병렬 데이터 웨어하우스 토폴로지** 메뉴를 클릭는 **서비스 상태** 탭을 클릭 **중지 지역** PDW 서비스를 중지 합니다.  
  
4.  없으면 HDInsight 지역이 아래에서 **HDInsight 토폴로지** 메뉴를 클릭는 **서비스 상태** 탭을 클릭 **중지 지역** HDInsight 서비스를 중지 합니다.  
  
5.  연결할 ***appliance_domain *-HST01** 기기 도메인 관리자 계정 사용 하 여 로그인 합니다.  
  
6.  사용 하는 **장애 조치 클러스터 관리자** 에 연결 된 ***appliance_domain *-WFOHST01** 탐색 창에서을 클릭 하 고 자동으로 연결 하는 경우 클러스터 **역할**. 에 **역할** 창:  
  
    1.  가상 컴퓨터의 모든 여러 개 선택 합니다. 선택 하 고 마우스 **종료**합니다.  
  
    2.  모든 선택한 Vm 종료 하 고 완료 될 때까지 기다립니다.  
  
7.  HDInsight 지역이 인 경우  
  
    1.  HDInsight 클러스터에 연결 합니다. 이렇게 하려면 마우스 오른쪽 단추로 클릭 **장애 조치 클러스터 관리자**선택, **클러스터에 연결**, 지정 ***appliance_domain *-WFOHST02** 클러스터 이름에 대 한 합니다.  
  
    2.  HDInsight 클러스터에서 클릭 **역할**합니다. 에 **역할** 창:  
  
        1.  모든 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 선택 다중 선택 **종료**합니다.  
  
        2.  가상 컴퓨터가 종료 될 때까지 기다립니다.  
  
8.  닫기는 **장애 조치 클러스터 관리자** 응용 프로그램입니다.  
  
9. 모든 서버를 제외 하 고 종료 ***appliance_domain *-HST01**합니다.  
  
10. 종료는 ***appliance_domain *-HST01** 서버입니다.  
  
11. 전원 Pdu (배전)를 종료 합니다.  
  
## <a name="PowerOn"></a>어플라이언스에서 전원  
  
### <a name="to-power-on-the-appliance"></a>어플라이언스에 시동  
  
> [!WARNING]  
> 나열 된 정확한 순서로 모든 단계를 수행 해야 하 고 다른 설명이 없는 각 단계는 다음 단계를 수행 하기 전에 완료 해야 합니다. 잘못 된 순서로 또는 각 단계를 완료 될 때까지 기다리지 않고 단계를 수행 시작 오류가 발생할 수 있습니다.  
  
1.  전원을 켜고 배전 장치 (PDU의), 스위치에 대 한 대기를 자동으로 시작 합니다.  
  
2.  전원을 켜거나는 ***appliance_domain *-HST01** 서버입니다.  
  
3.  에 로그인 ***appliance_domain *-HST01** 기기 도메인 관리자로 도메인입니다.  
  
4.  시작 된 **Hyper-v 관리자** 프로그램 (**virtmgmt.msc**)에 연결 하 고 ***appliance_domain *-HST01** 기본적으로 연결 되어 있지 합니다.  
  
    1.  때문에 이름으로 연결할 수 없는 경우는 ***PDW_region *-AD01** 은 실행 되 고 있지 IP 주소를 사용 하 여 연결 시도 합니다.  
  
    2.  에 **가상 컴퓨터** 창 찾기 ***PDW_region *-AD01** 실행 되는지 확인 합니다. 그렇지 않은 경우이 VM을 시작 하 고 완전히 시작 될 때까지 기다렸다가 합니다.  
  
5.  나머지 기기에서 서버를 켭니다.  
  
6.  에 있는 동안 **HST01** 에서 기기 도메인 관리자로 로그온 **Hyper-v 관리자**:  
  
    1.  연결할 ***appliance_domain *-HST02**합니다.  
  
    2.  에 **가상 컴퓨터** 창 찾기 ***PDW_region *-AD02** 실행 되는지 확인 합니다.  그렇지 않은 경우이 VM을 시작 하 고 완전히 시작 될 때까지 기다렸다가 합니다.  
  
7.  사용 하 여는 **장애 조치 클러스터 관리자** 에 연결 된 ***appliance_domain *-WFOHST01** 클러스터를 자동으로 연결 하는 경우 선택한 다음는 **탐색** 창에서 클릭 **역할**합니다. 에 **역할** 창:  
  
    1.  모든 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 다중 선택 **시작**합니다.  
  
    2.  모든 선택한 Vm에는 다음 단계로 진행 하기 전에 시작 될 때까지 기다립니다.  
  
    3.  장애 조치 하는 Vm에 대 한 필요한 경우 종료할 이동 하 고 적절 한 기본 호스트에서 다시 시작 합니다.  
  
8.  어플라이언스에 HDInsight 지역이 있는 경우에 HDInsight 클러스터에 연결 합니다. (이렇게 하려면 마우스 오른쪽 단추로 클릭 **장애 조치 클러스터 관리자**선택, **클러스터에 연결**, 지정 ***appliance_domain *-WFOHST01** 클러스터 이름에 대 한 합니다.)  
  
    1.  HDInsight 클러스터에서 클릭 **역할**합니다. 에 **역할** 창.  
  
        1.  모든 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 선택 다중 선택 **시작**,  
  
        2.  모든 선택한 Vm에는 다음 단계로 진행 하기 전에 시작 될 때까지 기다립니다.  
  
        3.  장애 조치 하는 Vm에 대 한 필요한 경우 종료할 이동 하 고 적절 한 기본 호스트에서 다시 시작 합니다.  
  
9. 연결 끊기 **HST01** 하려는 경우.  
  
10. 연결할 ***PDW_region *-CTL01** 기기 도메인 관리자 계정을 사용 합니다.  
  
11. 실행 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` 시작 하는 **Configuration Manager**합니다.  
  
12. 에 **Configuration Manager**에 **병렬 데이터 웨어하우스 토폴로지** 메뉴를 클릭는 **서비스 상태** 탭을 클릭 **시작 영역**PDW 서비스를 시작 합니다.  
  
13. 어플라이언스에 HDInsight 토폴로지 메뉴에는 HDInsight 영역에 있는 경우 클릭는 **서비스 상태** 탭을 클릭 **시작 영역** HDInsight 서비스를 시작 합니다.  
  
### <a name="to-verify-the-appliance-health"></a>어플라이언스 상태 확인  
기기 시작 된 후에 열은 **관리 콘솔** 오류 상태를 나타낼 수 있는 경고에 대 한 상태 페이지를 확인 합니다. 자세한 내용은 참조 [관리 콘솔을 사용 하 여 어플라이언스에 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[어플라이언스 관리 작업 &#40;분석 플랫폼 시스템&#41;](appliance-management-tasks.md)  
  
