---
title: InfiniBand-분석 플랫폼 시스템 구성 | Microsoft Docs
description: 하는 제어 노드에 병렬 데이터 웨어하우스 (PDW)에 연결 하는 데 비 어플라이언스 클라이언트 서버에 InfiniBand 네트워크 어댑터를 구성 하는 방법에 설명 합니다. 로드, 백업, 및 기타 프로세스 활성 InfiniBand 네트워크에 자동으로 연결 되도록 하 고 고가용성을 위해 기본 연결에 대 한 다음이 지침을 사용 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8e67d63e7bb4bded0bd19e5db4a0b7faddb80977
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539023"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 InfiniBand 네트워크 어댑터 구성
하는 제어 노드에 병렬 데이터 웨어하우스 (PDW)에 연결 하는 데 비 어플라이언스 클라이언트 서버에 InfiniBand 네트워크 어댑터를 구성 하는 방법에 설명 합니다. 로드, 백업, 및 기타 프로세스 활성 InfiniBand 네트워크에 자동으로 연결 되도록 하 고 고가용성을 위해 기본 연결에 대 한 다음이 지침을 사용 합니다.  
  
## <a name="Basics"></a>설명  
이러한 지침은 찾고 다음 올바른 InfiniBand IP 주소 및 서브넷 마스크 서버에 설정할 InfiniBand 연결 하는 방법을 보여 줍니다. 또한 활성 InfiniBand 네트워크로 연결 확인 되도록 APS 기기 DNS를 사용 하려면 서버를 설정 하는 방법에 대해서도 설명 합니다.  
  
고가용성을 위해 APS에 두 개의 InfiniBand 네트워크, 활성 및 수동 하나 있습니다. 각 InfiniBand 네트워크에는 제어 노드에 대해 다른 IP 주소입니다. 활성 InfiniBand 네트워크 작동이 중지 된 경우 수동 InfiniBand 네트워크 활성 네트워크가 됩니다. 이 경우 스크립트 또는 프로세스를 자동으로 연결 활성 InfiniBand 네트워크에 스크립트 매개 변수를 변경 하지 않고 합니다.  
  
특히,이 있습니다를 문서:  
  
1.  서버 APS DNS의 InfiniBand IP 주소 찾기 (appliance_domain AD01 및 appliance_domain *-AD02). 이 작업을 수행 하려면 AD01 및 AD02 서버에 로그인 하 고 각 InfiniBand 네트워크에 대 한 IP 주소를 가져옵니다. AD 노드 InfiniBand IP 주소는 DNS IP 주소입니다.  
  
2.  APS InfiniBand 네트워크에서 사용 가능한 IP 주소를 사용 하도록 각 네트워크 어댑터를 구성 합니다.  
  
    1.  2 개의 InfiniBand 네트워크 어댑터를 사용 하도록 설정한 경우에 TeamIB2 라는 두 번째 InfiniBand 네트워크 TeamIB1, 및 사용 가능한 IP 주소와 다른 어댑터 라는 첫 번째 InfiniBand 네트워크에서 사용 가능한 IP 주소와 어댑터 하나를 구성 합니다. 기본 설정된 DNS 서버 및 appliance_domain AD02 TeamIB1 IP 주소 사용 appliance_domain AD01 TeamIB1 TeamIB1 네트워크 어댑터에 대 한 대체 DNS 서버 IP 주소입니다. 기본 설정된 DNS 서버 및 appliance_domain AD02 TeamIB2 IP 주소 사용 appliance_domain AD01 TeamIB2 TeamIB2 네트워크 어댑터에 대 한 대체 DNS 서버 IP 주소입니다.  
  
    2.  InfiniBand 네트워크 어댑터가 하나만 있는 경우에 InfiniBand 네트워크 중 하나에서 사용 가능한 IP 주소와 어댑터를 구성 합니다. 다음 appliance_domain AD01 TeamIB1 및 appliance_domain AD02 TeamIB1 중 하나를 사용 하 여 사용 하거나 appliance_domain AD01 TeamIB2와 appliance_domain AD02 TeamIB2 동일한 더 작은 값이 어댑터에는 기본 설정 및 대체 DNS 서버 구성 각각의 기본 설정으로 구성 된 어댑터와 대체 DNS 서버와 네트워크입니다.  
  
3.  활성 InfiniBand 네트워크에 연결을 해결 하려면 APS DNS 서버를 사용 하도록 InfiniBand 네트워크 어댑터를 구성 합니다.  
  
    1.  이 옵션을 구성 하려면 클라이언트 서버에 DNS 접미사 목록 맨 앞으로 기기 도메인 DNS 접미사를 추가 하려면 고급 TCP/IP 설정을 사용 합니다. 네트워크 어댑터; 중 하나에 구성 하면 두 어댑터에 설정이 적용 됩니다.  
  
InfiniBand 네트워크 어댑터를 구성 했으면 클라이언트 프로세스에 연결할 수는 제어 노드에 InfiniBand 네트워크에서 사용 하 여 `PDW_region-SQLCTL01` 서버 주소에 대 한 합니다. 분석 플랫폼 시스템 DNS 접미사를 추가 하는 서버 또는 전체 주소를 입력할 수 있는 `PDW_region-SQLCTL01.appliance_domain.pdw.local`합니다.  
  
예를 들어 PDW 영역 이름을 MyPDW 이며 응용 프로그램 이름 MyAPS, 데이터를 로드 하기 위한 dwloader 서버 사양에는 다음 중 하나입니다.  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>시작하기 전 주의 사항  
  
### <a name="requirements"></a>요구 사항  
AD01 노드에 로그인 할 APS 기기 도메인 계정이 필요 합니다. 예를 들어 F12345 * \Administrator 합니다.  
  
네트워크 어댑터를 구성할 수 있는 권한을 가진 클라이언트 서버에 Windows 계정이 필요 합니다.  
  
### <a name="prerequisites"></a>필수 구성 요소  
이러한 지침에는 클라이언트 서버 이미 racked 되 고 어플라이언스의 InfiniBand 네트워크 케이블이 연결 가정 합니다. 랙 및 케이블 지침 [를 획득 하 고 로드 하는 서버를 구성](acquire-and-configure-loading-server.md)합니다.  
  
### <a name="general-remarks"></a>일반적인 주의 사항  
SQLCTL01를 사용 하 여 DNS 분석 플랫폼 시스템에는 제어 노드에 클라이언트 서버 활성 InfiniBand 네트워크를 사용 하 여 연결 합니다. 이; 연결에 적용 됩니다. InfiniBand 네트워크에서 부하 또는 백업 하는 동안 작동이 중지 된 경우 프로세스를 다시 시작 해야 합니다.  
  
비즈니스 요구 사항에 맞게, 비 어플라이언스 작업 그룹 또는 Windows 도메인 사용자 고유의 클라이언트 서버를 조인할 수 있습니다.  
  
## <a name="Sec1"></a>1 단계: 기기를 InfiniBand 네트워크 설정을 가져오려면  
*어플라이언스에 InfiniBand 네트워크 설정을 가져오려면*  
  
1.  로그인 기기 AD01 노드 appliance_domain\Administrator 계정을 사용 하 여 합니다.  
  
2.  어플라이언스 AD01 노드에서 제어판을 열고, 네트워크 및 인터넷, 선택 네트워크 및 공유 센터 *를 선택한 후 어댑터 설정 변경 합니다.  
  
3.  네트워크 연결 창에서 팀 IB1를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![관리 노드에서의 InfiniBand 연결](media/network-teamib.png "관리 노드에서의 InfiniBand 연결")  
  
4.  에 대 한 값은 인터넷 프로토콜 버전 4 (TCP/IPv4) 속성 창에서 기록 된 **IP 주소** 및 **서브넷 마스크**합니다.  IP 주소는 ***appliance_domain *-AD01** 노드는 분석 플랫폼 시스템 DNS 서버의 IP 주소입니다.  
  
5.  TeamIB1 어댑터에 대해 1-5 위의 단계를 반복 ***appliance_domain *-AD02** 서버입니다.  
  
    ![PDW 관리 노드 InfiniBand 1 속성](media/network-ip1-properties.png "PDW 관리 노드 InfiniBand 1 속성")  
  
6.  창을 닫으려면 취소 클릭 합니다.  
  
7.  TeamIB1 네트워크에서 사용 되지 않는 IP 주소를 찾아서 적어 둡니다.  
  
    사용 되지 않는 IP 주소를 확인 하려면 명령 창을 열고 어플라이언스에 대 한 주소 범위 내의 IP 주소를 ping 해 봅니다. 이 예제에서는 TeamIB1 네트워크의 IP 주소가 172.16.14.30를 되었습니다. 사용 되지 않는 172.16.14로 시작 하는 IP 주소를 찾습니다. 예를 들어 명령줄에서 "172.16.14.254 ping"를 입력 합니다. Ping 요청 실패할 경우 IP 주소를 사용할 수 있습니다.  
  
8.  TeamIB2에 대 한 동일한 작업을 수행 합니다. 에 * 네트워크 연결 창 팀 IB2를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
9. 인터넷 프로토콜 버전 4 (TCP/IPv4) 속성 창에서 TeamIB2에 대 한 IP 주소 및 서브넷 마스크의 값을 기록해 둡니다.  
  
10. Appliance_domain AD02 서버의 TeamIB2 어댑터에 대 한 8-9 위의 단계를 반복 합니다.  
  
    ![TeamIB2에 대 한 속성](media/network-ip2-properties.png "TeamIB2에 대 한 속성")  
  
11. 사용 되지 않는 IP 주소를 찾을 **TeamIB2** 고 네트워크에 기록 합니다.  
  
    사용 되지 않는 IP 주소를 확인 하려면 명령 창을 열고 어플라이언스에 대 한 주소 범위 내의 IP 주소를 ping 해 봅니다. 이 예제에서는 TeamIB2 네트워크의 IP 주소가 172.16.18.30를 되었습니다. 사용 되지 않는 172.16.18로 시작 하는 IP 주소를 찾습니다. 예를 들어 명령줄에서 "172.16.18.254 ping"를 입력 합니다. Ping 요청 실패할 경우 IP 주소를 사용할 수 있습니다.  
  
## <a name="Sec2"></a>2 단계: 클라이언트 서버에 InfiniBand 네트워크 어댑터 설정 구성  

### <a name="notes"></a>참고  
  
-   이러한 단계에 서버 APS DNS 서버를 등록 하는 방법을 보여 줍니다.  
  
-   네트워크 요구 사항에 맞게, 비 어플라이언스 작업 그룹 또는 Windows 도메인 사용자 고유의 클라이언트 서버를 조인할 수 있습니다.  
  
-   지침에 각 서버에 두 개의 네트워크 어댑터 구성 단계별로 실행 합니다.  네트워크 어댑터 두 개 있습니다, 네트워크 어댑터에 구성 하 고 다음 대체 DNS 서버로 두 번째 DNS IP 주소를 추가 하도록 네트워크 중 하나를 선택 합니다.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>클라이언트 서버에 InfiniBand 네트워크 어댑터 설정을 구성 하려면  
  
1.  InfiniBand 네트워크에 로드, 백업 또는 다른 클라이언트 서버 어플라이언스에서는 Windows 관리자로 로그인 합니다.  
  
2.  제어 창 * 네트워크 및 공유 센터를 찾아서 어댑터 설정 변경을 선택 합니다.  
  
### <a name="to-configure-the-first-network-adapter"></a>첫 번째 네트워크 어댑터를 구성 하려면  
  
1.  네트워크 연결 창에서 Mellanox 어댑터에 대 한 알 수 없는 네트워크 슬롯 중 하나를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![InfiniBand 네트워크 선택](media/network-connections.png "InfiniBand 네트워크 선택")  
  
2.  속성 창에서  
  
    1.  일반 탭에서 IP 주소를 TeamIB1에 대 한 ping 테스트에 가능한 것으로 확인 하는 IP 주소를 설정 합니다. 이 문서에서 사용 하 여 예제 값에 대 한 172.16.14.254에 입력 합니다.  
  
    2.  서브넷 마스크를 적어 TeamIB1에 대 한 서브넷 마스크를 설정 합니다.  
  
    3.  앞서 작성 appliance_domain *에서 TeamIB1의 IP 주소를 기본 설정 DNS 서버 설정-AD01 노드.  
  
    4.  앞서 작성 appliance_domain *에서 TeamIB1의 IP 주소로 대체 DNS 서버 설정-AD02 노드.  
  
        ![InfiniBand 1 네트워크 어댑터 속성](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  변경 내용을 적용 하려면 확인을 클릭 합니다.  
  
### <a name="to-configure-the-second-network-adapter"></a>두 번째 네트워크 어댑터를 구성 하려면  
  
1.  네트워크 어댑터 두 개 있는 경우이 섹션을 건너뜁니다.  
  
2.  네트워크 연결 창에서 두 번째 식별 되지 않은 네트워크 슬롯 Mellanox 어댑터에 대 한 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
    ![InfiniBand 네트워크 선택](media/network-connections.png "InfiniBand 네트워크 선택")  
  
3.  속성 창에서  
  
    1.  일반 탭에서 IP 주소를 TeamIB2에 대 한 ping 테스트에 가능한 것으로 확인 하는 IP 주소를 설정 합니다. 이 문서에서 사용 하 여 예제 값에 대 한 172.16.18.254에 입력 합니다.  
  
    2.  서브넷 마스크를 적어 TeamIB2에 대 한 서브넷 마스크를 설정 합니다.  
  
    3.  앞서 작성 appliance_domain *에서 TeamIB2의 IP 주소를 기본 설정 DNS 서버 설정-AD01 노드.  
  
    4.  앞서 작성 appliance_domain *에서 TeamIB2의 IP 주소로 대체 DNS 서버 설정-AD02 노드.  
  
        > [!NOTE]  
        > 하나만 있는 경우 네트워크 어댑터, 기본 및 각각 사용 하 여 어플라이언스에 AD01 TeamIB1와 어플라이언스 AD02 TeamIB1 중 하나는 기본 설정 및 대체 DNS 서버, 대체 DNS 서버를 구성 또는 어플라이언스 AD01 TeamIB2를 사용 하 여 하나 및 기본 설정으로 AD02 TeamIB2 기기 및 여부에 따라 대체 DNS 서버는 AD 가상 컴퓨터 장애 조치 되었습니다.  
  
        ![InfiniBand 1 네트워크 어댑터 속성](media/network-ib1-properties.png "InfiniBand 1 네트워크 어댑터 속성")  
  
    5.  변경 내용을 적용 하려면 확인을 클릭 합니다.  
  
### <a name="to-configure-the-dns-suffix"></a>DNS 접미사를 구성 하려면  
  
1.  네트워크 연결 창에서 Mellanox 어댑터에 대 한 네트워크 슬롯 중 하나를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.  
  
2.  에 고급을 클릭 하십시오... 단추를 선택합니다.  
  
3.  고급 TCP/IP 설정 창에서 추가 DNS 접미사 (순서 대로) 옵션 이러한가 되지 회색 경우 확인 상자 호출 다음 DNS 접미사 추가 순서에 따라:, 기기 도메인 접미사를 선택 하 고 추가 클릭 하 고 있습니다... 어플라이언스 도메인 접미사는 `appliance_domain.local`  
  
4.  다음이 DNS 접미사 (순서 대로)는 추가 하는 경우: 옵션이 회색, HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient 레지스트리 키를 수정 하 여이 서버에 APS 도메인을 추가할 수 있습니다.  
  
    ![TCP/IP 설정](media/network-tcpip.png "TCP/IP 설정")  
  
5.  더 빠른 주소 확인에 대 한 기기 접미사 목록의 맨 위로 이동 하는 것이 좋습니다.  
  
6.  확인을 클릭합니다.  
  
7.  이제, 연결할 수 있습니다 기기 Infiniband 네트워크를 사용 하 여 `PDW_region-SQLCTL01.appliance_domain.local`, 또는 단순히 `appliance_domain-SQLCTL01`합니다. 전체 이름 및 DNS 접미사를 연결 하면 연결을 더 빠르게 설정할 수 있습니다.  
  
    어플라이언스에 대 한 예 이라는 MyAPS MyPDW PDW 영역으로 입력 합니다.  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>관련 항목:  
[획득 하 고 로드 하는 서버를 구성 합니다. ](acquire-and-configure-loading-server.md)  
  
