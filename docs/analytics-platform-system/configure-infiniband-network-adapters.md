---
title: Analytics Platform System InfiniBand-구성 | Microsoft Docs
description: 병렬 데이터 웨어하우스 (PDW)에서 제어 노드에 연결 하려면 클라이언트 비 어플라이언스 서버의 InfiniBand 네트워크 어댑터를 구성 하는 방법을 설명 합니다. 자동으로 활성 InfiniBand 네트워크 로드, 백업 및 다른 프로세스에 연결할 수 있도록 기본 연결을 고가용성을 위해 다음이 지침을 따르세요.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e0e0ed3aea02ae8a79d89871f6849b1cbf40c9d0
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169342"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Analytics Platform System에 대 한 InfiniBand 네트워크 어댑터를 구성 합니다.
병렬 데이터 웨어하우스 (PDW)에서 제어 노드에 연결 하려면 클라이언트 비 어플라이언스 서버의 InfiniBand 네트워크 어댑터를 구성 하는 방법을 설명 합니다. 자동으로 활성 InfiniBand 네트워크 로드, 백업 및 다른 프로세스에 연결할 수 있도록 기본 연결을 고가용성을 위해 다음이 지침을 따르세요.  
  
## <a name="Basics"></a>설명  
이러한 지침 찾아 설정한 올바른 InfiniBand IP 주소 및 서브넷 마스크 InfiniBand 연결 된 서버에서 하는 방법을 보여 줍니다. 또한 active InfiniBand 네트워크에 대 한 연결 확인 되도록 DNS APS 어플라이언스를 사용 하도록 서버를 설정 하는 방법에도 설명 합니다.  
  
고가용성을 위해 AP에 두 개의 InfiniBand 네트워크, 활성 및 수동 하나 있습니다. 각 InfiniBand 네트워크에는 제어 노드에 대 한 다른 IP 주소에 있습니다. 활성 InfiniBand 네트워크가 다운 되 면 수동 InfiniBand 네트워크는 활성 네트워크가 됩니다. 이 문제가 발생 하면 스크립트 또는 프로세스를 자동으로 연결할 active InfiniBand 네트워크 스크립트 매개 변수를 변경 하지 않고 있습니다.  
  
특히이 하를 문서:  
  
1.  서버 AP dns InfiniBand IP 주소를 찾으려면 (appliance_domain AD01 및 appliance_domain *-AD02). 이 작업을 수행 하려면 AD01 및 AD02 서버에 로그인 하 고 각 InfiniBand 네트워크에 대 한 IP 주소를 가져옵니다. AD 노드 InfiniBand IP 주소는 DNS IP 주소입니다.  
  
2.  AP InfiniBand 네트워크에서 사용 가능한 IP 주소를 사용 하도록 각 네트워크 어댑터를 구성 합니다.  
  
    1.  2 개의 InfiniBand 네트워크 어댑터를 사용 하는 경우에 TeamIB2 이라고 하는 두 번째 InfiniBand 네트워크 TeamIB1, 및 사용 가능한 IP 주소를 사용 하 여 다른 어댑터 라고 하는 첫 번째 InfiniBand 네트워크에서 사용 가능한 IP 주소를 사용 하 여 하나의 어댑터를 구성 합니다. 기본 설정된 DNS 서버 및 appliance_domain AD02 TeamIB1 IP 주소 사용 appliance_domain AD01 TeamIB1 TeamIB1 네트워크 어댑터에 대 한 대체 DNS 서버 IP 주소입니다. 기본 설정된 DNS 서버 및 appliance_domain AD02 TeamIB2 IP 주소 사용 appliance_domain AD01 TeamIB2 TeamIB2 네트워크 어댑터에 대 한 대체 DNS 서버 IP 주소입니다.  
  
    2.  InfiniBand 네트워크 어댑터가 하나뿐인 경우에 InfiniBand 네트워크 중 하나에서 사용 가능한 IP 주소를 사용 하 여 어댑터를 구성 합니다. 다음 appliance_domain AD01 TeamIB1 및 appliance_domain AD02 TeamIB1 중 하나를 사용 하 여 사용 하거나 appliance_domain AD01 TeamIB2와 appliance_domain AD02 TeamIB2 동일한 더이 어댑터에는 기본 및 대체 DNS 서버 구성 각각의 기본 설정으로 구성 된 어댑터와 대체 DNS 서버 네트워크입니다.  
  
3.  AP DNS 서버 active InfiniBand 네트워크에 연결을 확인 하는 데 InfiniBand 네트워크 어댑터를 구성 합니다.  
  
    1.  이 설정을 구성 하려면 고급 TCP/IP 설정을 사용 하 여 클라이언트 서버에서 DNS 접미사 목록 맨 앞으로 어플라이언스 도메인 DNS 접미사를 추가 합니다. 이; 네트워크 어댑터 중 하나에서 구성 해야 설정을 모두 어댑터에 적용 됩니다.  
  
InfiniBand 네트워크 어댑터를 구성한 후 클라이언트 프로세스 수의 제어 노드 InfiniBand 네트워크를 사용 하 여 연결할 `PDW_region-SQLCTL01` 서버의 주소입니다. 서버에는 분석 플랫폼 시스템 DNS 접미사를 추가 하거나 되는 전체 주소를 입력할 수 있습니다 `PDW_region-SQLCTL01.appliance_domain.pdw.local`합니다.  
  
예를 들어 PDW 영역 이름을 MyPDW 이며 어플라이언스 이름이 MyAPS, 데이터를 로드 하기 위한 dwloader 서버 사양에 다음 중 하나입니다.  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
  
### <a name="requirements"></a>요구 사항  
APS 어플라이언스 도메인 계정을 AD01 노드에 로그인 해야 합니다. 예를 들어 F12345 * \Administrator 합니다.  
  
네트워크 어댑터를 구성할 수 있는 권한을 가진 클라이언트 서버에 대 한 Windows 계정이 필요 합니다.  
  
### <a name="prerequisites"></a>필수 구성 요소  
이러한 지침에는 클라이언트 서버 랙을 탑재 했으며 이미 이며 어플라이언스의 InfiniBand 네트워크를 케이블로 연결 가정 합니다. 랙 및 케이블 연결 지침은 참조 하세요 [로드 서버 획득 및 구성](acquire-and-configure-loading-server.md)합니다.  
  
### <a name="general-remarks"></a>일반적인 주의 사항  
SQLCTL01를 사용 하 여 DNS 분석 플랫폼 시스템 제어 노드에 클라이언트 서버 활성 InfiniBand 네트워크를 사용 하 여 연결 합니다. 이; 연결에 적용 됩니다. InfiniBand 네트워크를 로드 또는 백업 하는 동안 다운 되 면 프로세스를 다시 시작 해야 합니다.  
  
고유한 비즈니스 요구 사항에 고유한 비 어플라이언스 작업 그룹 또는 Windows 도메인에도 클라이언트 서버를 조인할 수 있습니다.  
  
## <a name="Sec1"></a>1 단계: 기기를 InfiniBand 네트워크 설정을 가져오려면  
*어플라이언스 InfiniBand 네트워크 설정을 가져오려면*  
  
1.  로그인 어플라이언스에 AD01 노드 appliance_domain\Administrator 계정을 사용 하 여 합니다.  
  
2.  어플라이언스 AD01 노드에서 제어판을 열고, 네트워크 및 인터넷, 선택 네트워크 및 공유 센터 *를 선택한 다음 선택 어댑터 설정 변경 합니다.  
  
3.  네트워크 연결 창에서 팀 IB1를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![관리 노드에서의 InfiniBand 연결](media/network-teamib.png "관리 노드에서의 InfiniBand 연결")  
  
4.  인터넷 프로토콜 버전 4 (Tcp/ipv4) 속성 창에서에 대 한 값을 적어 둡니다 합니다 **IP 주소** 하 고 **서브넷 마스크**합니다.  IP 주소를  **_어플라이언스\_도메인_-AD01** 노드는 분석 플랫폼 시스템 DNS 서버의 IP 주소입니다.  
  
5.  TeamIB1 어댑터에 대 한 위의 1-5 단계를 반복  **_어플라이언스\_도메인_-AD02** 서버.  
  
    ![PDW 관리 노드 InfiniBand 1 속성](media/network-ip1-properties.png "PDW 관리 노드 InfiniBand 1 속성")  
  
6.  창을 닫으려면 취소 클릭 합니다.  
  
7.  TeamIB1 네트워크에서 사용 되지 않는 IP 주소를 찾고 적어 둡니다.  
  
    사용 되지 않는 IP 주소를 찾으려면 명령 창을 열고 어플라이언스에 대 한 주소 범위 내의 IP 주소를 ping 해 봅니다. 이 예제에서는 TeamIB1 네트워크의 ip에서는 172.16.14.30입니다. 사용 되지 않는 172.16.14로 시작 하는 IP 주소를 찾습니다. 예를 들어 명령줄에서 "172.16.14.254 ping"를 입력 합니다. Ping 요청 실패할 경우 IP 주소는 사용할 수 있습니다.  
  
8.  TeamIB2의 동일한 작업을 수행 합니다. 에 * 네트워크 연결 창에서 팀 IB2를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
9. 인터넷 프로토콜 버전 4 (Tcp/ipv4) 속성 창에서 TeamIB2의 IP 주소 및 서브넷 마스크 값을 적어 둡니다.  
  
10. Appliance_domain AD02 서버의 TeamIB2 어댑터에 대 한 위의 8-9 단계를 반복 합니다.  
  
    ![TeamIB2의 속성](media/network-ip2-properties.png "TeamIB2의 속성")  
  
11. 사용 되지 않는 IP 주소를 찾을 합니다 **TeamIB2** 네트워크 및 적어 둡니다.  
  
    사용 되지 않는 IP 주소를 찾으려면 명령 창을 열고 어플라이언스에 대 한 주소 범위 내의 IP 주소를 ping 해 봅니다. 이 예제에서는 TeamIB2 네트워크의 ip에서는 172.16.18.30입니다. 사용 되지 않는 172.16.18로 시작 하는 IP 주소를 찾습니다. 예를 들어 명령줄에서 "172.16.18.254 ping"를 입력 합니다. Ping 요청 실패할 경우 IP 주소는 사용할 수 있습니다.  
  
## <a name="Sec2"></a>2 단계: 클라이언트 서버의 InfiniBand 네트워크 어댑터 설정 구성  

### <a name="notes"></a>참고  
  
-   이러한 단계 AP DNS 서버를 사용 하 여 서버를 등록 하는 방법을 보여 줍니다.  
  
-   네트워크 요구 사항에 맞게, 사용자 고유의 비 어플라이언스 작업 그룹 또는 Windows 도메인에도 클라이언트 서버를 조인할 수 있습니다.  
  
-   각 서버에서 두 개의 네트워크 어댑터를 구성 하는 과정 지침 단계입니다.  하나의 네트워크 어댑터에만 있는 경우 네트워크 어댑터에 구성 하 고 다음 대체 DNS 서버와 보조 DNS IP 주소를 추가 하려면 네트워크 중 하나를 선택 합니다.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>클라이언트가 서버의 InfiniBand 네트워크 어댑터 설정을 구성 하려면  
  
1.  InfiniBand 네트워크에 로드, 백업 또는 어플라이언스에서 다른 클라이언트 서버에 Windows 관리자로 로그인 합니다.  
  
2.  열 컨트롤 창 *, 네트워크 및 공유 센터를 선택 하 고 어댑터 설정 변경을 선택 합니다.  
  
### <a name="to-configure-the-first-network-adapter"></a>첫 번째 네트워크 어댑터를 구성 하려면  
  
1.  네트워크 연결 창에서 알 수 없는 네트워크 슬롯 중 하나에서 Mellanox 어댑터에 대 한 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![InfiniBand 네트워크를 선택](media/network-connections.png "InfiniBand 네트워크를 선택 합니다.")  
  
2.  속성 창에서  
  
    1.  일반 탭의 TeamIB1 ping 테스트에서 사용 가능한 것으로 확인 된 IP 주소로 IP 주소를 설정 합니다. 이 문서에 사용 되는 예제 값 172.16.14.254에 입력 합니다.  
  
    2.  서브넷 마스크에서 기록해 둔 TeamIB1에 대 한 서브넷 마스크를 설정 합니다.  
  
    3.  이전 appliance_domain *에서 적어둔 TeamIB1의 IP 주소를 기본 설정 DNS 서버 설정-AD01 노드.  
  
    4.  이전 appliance_domain *에서 적어둔 TeamIB1의 IP 주소로 대체 DNS 서버 설정-AD02 노드.  
  
        ![InfiniBand 1 네트워크 어댑터 속성](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  변경 내용을 적용 하려면 확인을 클릭 합니다.  
  
### <a name="to-configure-the-second-network-adapter"></a>두 번째 네트워크 어댑터를 구성 하려면  
  
1.  하나의 네트워크 어댑터 하나만 있는 경우이 섹션을 건너뜁니다.  
  
2.  네트워크 연결 창에서 두 번째 알 수 없는 네트워크 슬롯 Mellanox 어댑터에 대 한 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![InfiniBand 네트워크를 선택](media/network-connections.png "InfiniBand 네트워크를 선택 합니다.")  
  
3.  속성 창에서  
  
    1.  일반 탭의 TeamIB2의 ping 테스트에서 사용 가능한 것으로 확인 된 IP 주소로 IP 주소를 설정 합니다. 이 문서에 사용 되는 예제 값 172.16.18.254에 입력 합니다.  
  
    2.  서브넷 마스크에서 기록해 둔 TeamIB2의 서브넷 마스크를 설정 합니다.  
  
    3.  이전 appliance_domain *에서 적어둔 TeamIB2의 IP 주소를 기본 설정 DNS 서버 설정-AD01 노드.  
  
    4.  이전 appliance_domain *에서 적어둔 TeamIB2의 IP 주소로 대체 DNS 서버 설정-AD02 노드.  
  
        > [!NOTE]  
        > 하나만 있는 네트워크 어댑터, 구성 된 기본 및 대체 DNS 서버를 사용 하 여 어플라이언스 AD01 TeamIB1 및 어플라이언스 AD02 TeamIB1 중 하나는 기본 및 대체 DNS 서버 각각 또는 AD01 TeamIB2 어플라이언스를 사용 하는 경우 및 원하는으로 AD02 TeamIB2 어플라이언스 및 경우에 따라 대체 DNS 서버는 AD 가상 컴퓨터 장애 조치 되었습니다.  
  
        ![InfiniBand 1 네트워크 어댑터 속성](media/network-ib1-properties.png "InfiniBand 1 네트워크 어댑터 속성")  
  
    5.  변경 내용을 적용 하려면 확인을 클릭 합니다.  
  
### <a name="to-configure-the-dns-suffix"></a>DNS 접미사를 구성 하려면  
  
1.  네트워크 연결 창에서 Mellanox 어댑터에 대 한 네트워크 슬롯 중 하나를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
2.  클릭 된 고급... 단추를 선택합니다.  
  
3.  고급 TCP/IP 설정 창에서 추가 이러한 DNS 접미사 (순서 대로) 옵션은 없습니다 회색으로 표시 하는 경우 체크 상자를 호출 다음 DNS 접미사 추가 (순서로 정렬): 어플라이언스 도메인 접미사를 선택 하 고 추가 클릭 하는 중... 어플라이언스 도메인 접미사가 `appliance_domain.local`  
  
4.  이러한 DNS 접미사 (순서 대로)를 추가 하는 경우: 옵션이 회색, HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient 레지스트리 키를 수정 하 여이 서버에 APS 도메인을 추가할 수 있습니다.  
  
    ![TCP/IP 설정을](media/network-tcpip.png "TCP/IP 설정")  
  
5.  빠른 주소 확인에 대 한 어플라이언스 접미사 목록의 맨 위로 이동 하는 것이 좋습니다.  
  
6.  확인을 클릭합니다.  
  
7.  이제 있습니다 수 어플라이언스의 Infiniband 네트워크를 사용 하 여 연결 `PDW_region-SQLCTL01.appliance_domain.local`, 또는 단순히 `appliance_domain-SQLCTL01`합니다. 전체 이름 및 DNS 접미사를 사용 하 여 연결 하는 경우 연결을 빠르게 설정 될 수 있습니다.  
  
    어플라이언스 예 MyAPS MyPDW PDW 영역 이라는 됩니다.  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>관련 항목  
[로드 서버 획득 및 구성 ](acquire-and-configure-loading-server.md)  
  
