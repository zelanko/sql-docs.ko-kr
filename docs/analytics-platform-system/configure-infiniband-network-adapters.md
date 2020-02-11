---
title: InfiniBand 구성
description: PDW (병렬 데이터 웨어하우스)의 제어 노드에 연결 하도록 비 어플라이언스 클라이언트 서버에서 InfiniBand 네트워크 어댑터를 구성 하는 방법을 설명 합니다. 기본 연결 및 고가용성을 위해 이러한 지침을 사용 하 여 로드, 백업 및 기타 프로세스가 활성 InfiniBand 네트워크에 자동으로 연결 되도록 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401288"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Analytics Platform System에 대 한 InfiniBand 네트워크 어댑터 구성
PDW (병렬 데이터 웨어하우스)의 제어 노드에 연결 하도록 비 어플라이언스 클라이언트 서버에서 InfiniBand 네트워크 어댑터를 구성 하는 방법을 설명 합니다. 기본 연결 및 고가용성을 위해 이러한 지침을 사용 하 여 로드, 백업 및 기타 프로세스가 활성 InfiniBand 네트워크에 자동으로 연결 되도록 합니다.  
  
## <a name="Basics"></a>Description  
이 지침에서는 InfiniBand 연결 된 서버에서 올바른 InfiniBand IP 주소 및 서브넷 마스크를 찾아서 설정 하는 방법을 보여 줍니다. 또한 연결이 활성 InfiniBand 네트워크로 확인 되도록 서버에서 APS 어플라이언스 DNS를 사용 하도록 설정 하는 방법을 설명 합니다.  
  
고가용성을 위해 APS에는 두 개의 InfiniBand 네트워크, 하나의 능동 및 하나의 passive가 있습니다. 각 InfiniBand 네트워크에는 제어 노드에 대해 서로 다른 IP 주소가 있습니다. 활성 InfiniBand 네트워크가 중단 되 면 passive InfiniBand 네트워크가 활성 네트워크가 됩니다. 이 경우 스크립트나 프로세스는 스크립트 매개 변수를 변경 하지 않고 활성 InfiniBand 네트워크에 자동으로 연결 됩니다.  
  
특히이 문서에서는 다음을 수행 합니다.  
  
1.  APS DNS 서버의 InfiniBand IP 주소를 찾습니다 (appliance_domain-AD01 및 appliance_domain *-AD02). 이렇게 하려면 AD01 및 AD02 서버에 로그인 하 고 각 InfiniBand 네트워크에 대 한 IP 주소를 가져옵니다. AD 노드의 InfiniBand IP 주소는 DNS IP 주소입니다.  
  
2.  AP InfiniBand 네트워크에서 사용 가능한 IP 주소를 사용 하도록 각 네트워크 어댑터를 구성 합니다.  
  
    1.  두 개의 InfiniBand 네트워크 어댑터를 사용 하는 경우 TeamIB1 이라는 첫 번째 InfiniBand 네트워크에서 사용 가능한 IP 주소를 사용 하 여 하나의 어댑터를 구성 하 고, 두 번째 InfiniBand 네트워크에서 사용 가능한 IP 주소를 사용 하 여 TeamIB2 라는 다른 어댑터를 구성 합니다. Appliance_domain-AD01 TeamIB1 IP 주소를 기본 설정 DNS 서버로 사용 하 고 appliance_domain-AD02 TeamIB1 IP 주소를 TeamIB1 네트워크 어댑터용 대체 DNS 서버로 사용 합니다. Appliance_domain-AD01 TeamIB2 IP 주소를 기본 설정 DNS 서버로 사용 하 고 appliance_domain-AD02 TeamIB2 IP 주소를 TeamIB2 네트워크 어댑터용 대체 DNS 서버로 사용 합니다.  
  
    2.  InfiniBand 네트워크 어댑터가 하나만 있는 경우 InfiniBand 네트워크 중 하나에서 사용 가능한 IP 주소를 사용 하 여 어댑터를 구성 합니다. 그런 다음 appliance_domain-AD01 TeamIB1 appliance_domain 및 AD02 TeamIB1를 사용 하 여이 어댑터에서 기본 설정 및 대체 DNS 서버를 구성 하 고, appliance_domain-AD01 TeamIB2 및 appliance_domain-AD02 TeamIB2 중 하나를 사용 하 여 구성 된 어댑터의 네트워크를 기본 설정 및 대체 DNS 서버로 각각 설정 합니다.  
  
3.  AP DNS 서버를 사용 하 여 활성 InfiniBand 네트워크에 대 한 연결을 확인 하도록 InfiniBand 네트워크 어댑터를 구성 합니다.  
  
    1.  이를 구성 하려면 고급 TCP/IP 설정을 사용 하 여 클라이언트 서버에서 DNS 접미사 목록의 시작 부분에 어플라이언스 도메인 DNS 접미사를 추가 합니다. 네트워크 어댑터 중 하나에만 구성 해야 합니다. 설정은 두 어댑터에 모두 적용 됩니다.  
  
InfiniBand 네트워크 어댑터를 구성한 후 클라이언트 프로세스는 서버 주소에 대해를 사용 `PDW_region-SQLCTL01` 하 여 InfiniBand 네트워크의 제어 노드에 연결할 수 있습니다. 서버에서 분석 플랫폼 시스템 DNS 접미사를 추가 하거나, 전체 주소를 입력할 수 있습니다 `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
예를 들어 PDW 지역 이름이 MyPDW이 고 어플라이언스 이름이 MyAPS 인 경우 데이터 로드에 대 한 dwloader 서버 사양은 다음 중 하나입니다.  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
  
### <a name="requirements"></a>요구 사항  
AD01 노드에 로그인 하려면 APS 어플라이언스 도메인 계정이 필요 합니다. 예: F12345 * \b  
  
클라이언트 서버에서 네트워크 어댑터를 구성할 수 있는 권한이 있는 Windows 계정이 필요 합니다.  
  
### <a name="prerequisites"></a>사전 요구 사항  
이 지침에서는 클라이언트 서버가 이미 racked 어플라이언스 InfiniBand 네트워크에 연결 되어 있다고 가정 합니다. Racking 및 케이블 연결 지침은 [로드 서버 가져오기 및 구성](acquire-and-configure-loading-server.md)을 참조 하세요.  
  
### <a name="general-remarks"></a>일반적인 주의 사항  
SQLCTL01를 사용 하면 분석 플랫폼 시스템 DNS가 활성 InfiniBand 네트워크를 사용 하 여 클라이언트 서버를 컨트롤 노드에 연결 합니다. 이는 연결 하기 위해서만 적용 됩니다. InfiniBand 네트워크에서 로드 또는 백업 중에 작동이 중단 되 면 프로세스를 다시 시작 해야 합니다.  
  
자신의 비즈니스 요구 사항을 충족 하기 위해 클라이언트 서버를 사용자의 비 어플라이언스 작업 그룹 또는 Windows 도메인에 조인할 수도 있습니다.  
  
## <a name="Sec1"></a>1 단계: 어플라이언스 InfiniBand 네트워크 설정 가져오기  
*어플라이언스 InfiniBand 네트워크 설정을 가져오려면*  
  
1.  Appliance_domain \Administrator 계정을 사용 하 여 어플라이언스 AD01 노드에 로그인 합니다.  
  
2.  어플라이언스 AD01 노드에서 제어판을 열고 네트워크 및 인터넷을 선택 하 고 네트워크 및 공유 센터 *를 선택한 후 어댑터 설정 변경을 선택 합니다.  
  
3.  네트워크 연결 창에서 Team IB1를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![관리 노드에 대 한 InfiniBand 연결](media/network-teamib.png "관리 노드에 대 한 InfiniBand 연결")  
  
4.  인터넷 프로토콜 버전 4 (TCP/IPv4) 속성 창에서 **IP 주소** 및 **서브넷 마스크**에 대 한 값을 기록 합니다.  ** _어플라이언스\_도메인_AD01** 노드의 IP 주소는 분석 플랫폼 시스템 DNS 서버의 ip 주소입니다.  
  
5.  ** _어플라이언스\__ AD02** 서버에서 TeamIB1 어댑터에 대해 위의 1-5 단계를 반복 합니다.  
  
    ![PDW 관리 노드 InfiniBand 1 속성](media/network-ip1-properties.png "PDW 관리 노드 InfiniBand 1 속성")  
  
6.  취소를 클릭 하 여 창을 닫습니다.  
  
7.  TeamIB1 네트워크에서 사용 되지 않는 IP 주소를 찾아서 기록 합니다.  
  
    사용 하지 않는 IP 주소를 찾으려면 명령 창을 열고 어플라이언스의 주소 범위 내에 있는 IP 주소를 ping 해 봅니다. 이 예에서는 TeamIB1 네트워크의 IP 주소가 172.16.14.30입니다. 사용 되지 않는 172.16.14로 시작 하는 IP 주소를 찾습니다. 예를 들어 명령줄에서 "ping 172.16.14.254"를 입력 합니다. Ping 요청이 실패 하는 경우 IP 주소를 사용할 수 있습니다.  
  
8.  TeamIB2에 대해 동일한 작업을 수행 합니다. * 네트워크 연결 창에서 Team IB2를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
9. 인터넷 프로토콜 버전 4 (TCP/IPv4) 속성 창에서 TeamIB2의 IP 주소 및 서브넷 마스크 값을 기록 합니다.  
  
10. Appliance_domain-AD02 server의 TeamIB2 어댑터에 대해 위의 8-9 단계를 반복 합니다.  
  
    ![TeamIB2의 속성](media/network-ip2-properties.png "TeamIB2의 속성")  
  
11. **TeamIB2** 네트워크에서 사용 되지 않는 IP 주소를 찾아서 기록 합니다.  
  
    사용 하지 않는 IP 주소를 찾으려면 명령 창을 열고 어플라이언스의 주소 범위 내에 있는 IP 주소를 ping 해 봅니다. 이 예에서는 TeamIB2 네트워크의 IP 주소가 172.16.18.30입니다. 사용 되지 않는 172.16.18로 시작 하는 IP 주소를 찾습니다. 예를 들어 명령줄에서 "ping 172.16.18.254"를 입력 합니다. Ping 요청이 실패 하는 경우 IP 주소를 사용할 수 있습니다.  
  
## <a name="Sec2"></a>2 단계: 클라이언트 서버에서 InfiniBand 네트워크 어댑터 설정 구성  

### <a name="notes"></a>메모  
  
-   이러한 단계에서는 AP DNS 서버에 서버를 등록 하는 방법을 보여 줍니다.  
  
-   사용자 고유의 네트워크 요구를 충족 하기 위해 클라이언트 서버를 사용자의 비 어플라이언스 작업 그룹 또는 Windows 도메인에 조인할 수도 있습니다.  
  
-   지침에서는 각 서버에서 두 개의 네트워크 어댑터를 구성 하는 단계를 안내 합니다.  네트워크 어댑터가 하나만 있는 경우 네트워크 어댑터에서 구성할 네트워크 중 하나를 선택 하 고 두 번째 DNS IP 주소를 대체 DNS 서버로 추가 합니다.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>클라이언트 서버에서 InfiniBand 네트워크 어댑터 설정을 구성 하려면  
  
1.  기기 InfiniBand 네트워크에서 로드, 백업 또는 기타 클라이언트 서버에 Windows 관리자로 로그인 합니다.  
  
2.  제어 창 *을 열고 네트워크 및 공유 센터를 선택한 다음 어댑터 설정 변경을 선택 합니다.  
  
### <a name="to-configure-the-first-network-adapter"></a>첫 번째 네트워크 어댑터를 구성 하려면  
  
1.  네트워크 연결 창에서 Mellanox 어댑터에 대 한 미확인 네트워크 슬롯 중 하나를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![InfiniBand 네트워크를 선택합니다.](media/network-connections.png "InfiniBand 네트워크를 선택합니다.")  
  
2.  속성 창  
  
    1.  일반 탭에서 IP 주소를 TeamIB1에 대 한 ping 테스트에서 사용 가능한 것으로 확인 한 IP 주소로 설정 합니다. 이 문서에서 사용 되는 예제 값에 대해 172.16.14.254를 입력 합니다.  
  
    2.  TeamIB1에 대해 적어 둔 서브넷 마스크에 서브넷 마스크를 설정 합니다.  
  
    3.  기본 설정 된 DNS 서버를 appliance_domain *-AD01 노드에서 앞에서 기록한 TeamIB1의 IP 주소로 설정 합니다.  
  
    4.  대체 DNS 서버를 appliance_domain *-AD02 노드에서 앞에서 기록한 TeamIB1의 IP 주소로 설정 합니다.  
  
        ![InfiniBand 1 네트워크 어댑터 속성](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  확인을 클릭 하 여 변경 내용을 적용 합니다.  
  
### <a name="to-configure-the-second-network-adapter"></a>두 번째 네트워크 어댑터를 구성 하려면  
  
1.  네트워크 어댑터가 하나뿐인 경우이 섹션을 건너뜁니다.  
  
2.  네트워크 연결 창에서 Mellanox 어댑터에 대 한 두 번째 미확인 네트워크 슬롯을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![InfiniBand 네트워크를 선택합니다.](media/network-connections.png "InfiniBand 네트워크를 선택합니다.")  
  
3.  속성 창  
  
    1.  일반 탭에서 IP 주소를 TeamIB2에 대 한 ping 테스트에서 사용 가능한 것으로 확인 한 IP 주소로 설정 합니다. 이 문서에서 사용 되는 예제 값에 대해 172.16.18.254를 입력 합니다.  
  
    2.  TeamIB2에 대해 적어 둔 서브넷 마스크에 서브넷 마스크를 설정 합니다.  
  
    3.  기본 설정 된 DNS 서버를 appliance_domain *-AD01 노드에서 앞에서 기록한 TeamIB2의 IP 주소로 설정 합니다.  
  
    4.  대체 DNS 서버를 appliance_domain *-AD02 노드에서 앞에서 기록한 TeamIB2의 IP 주소로 설정 합니다.  
  
        > [!NOTE]  
        > 네트워크 어댑터가 하나만 있는 경우 어플라이언스 AD01 TeamIB1 및 어플라이언스 AD02 TeamIB1를 각각 기본 설정 및 대체 DNS 서버로 사용 하 여 기본 설정 및 대체 DNS 서버를 구성 하거나, 어플라이언스 AD01 TeamIB2를 사용 합니다. AD 가상 머신이 장애 조치 (failover) 되었는지 여부에 따라 어플라이언스 AD02 TeamIB2를 기본 설정 및 대체 DNS 서버로 설정 합니다.  
  
        ![InfiniBand 1 네트워크 어댑터 속성](media/network-ib1-properties.png "InfiniBand 1 네트워크 어댑터 속성")  
  
    5.  확인을 클릭 하 여 변경 내용을 적용 합니다.  
  
### <a name="to-configure-the-dns-suffix"></a>DNS 접미사를 구성 하려면  
  
1.  네트워크 연결 창에서 Mellanox 어댑터에 대 한 네트워크 슬롯 중 하나를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
2.  고급 ...을 클릭 합니다. 단추만.  
  
3.  고급 TCP/IP 설정 창에서 다음 DNS 접미사 추가 (순서 대로) 옵션이 회색으로 표시 되지 않는 경우 다음 DNS 접미사 추가 (순서 대로) 라는 상자를 선택 하 고, 어플라이언스 도메인 접미사를 선택 하 고, 추가 ...를 클릭 합니다. 어플라이언스 도메인 접미사가`appliance_domain.local`  
  
4.  다음 DNS 접미사 추가 (순서 대로): 옵션이 회색으로 표시 된 경우 레지스트리 키 HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.를 수정 하 여이 서버에 APS 도메인을 추가할 수 있습니다.  
  
    ![TCP/IP 설정](media/network-tcpip.png "TCP/IP 설정")  
  
5.  주소 확인을 빠르게 하려면 목록 맨 위로 어플라이언스 접미사를 이동 하는 것이 좋습니다.  
  
6.  확인을 클릭합니다.  
  
7.  이제, 또는를 사용 `PDW_region-SQLCTL01.appliance_domain.local`하 여 어플라이언스 Infiniband 네트워크에 연결할 수 있습니다. `appliance_domain-SQLCTL01` 전체 이름 및 DNS 접미사를 사용 하 여 연결 하면 연결 속도가 빨라질 수 있습니다.  
  
    MyPDW PDW 지역이 있는 MyAPS 라는 어플라이언스에 대 한 예제:  
  
    -   MyPDW-SQLCTL01  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>참고 항목  
[로드 서버 가져오기 및 구성](acquire-and-configure-loading-server.md)  
  
