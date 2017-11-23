---
title: "Microsoft (SQL Server PDW) 원격 분석 피드백 보내기"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40a994f0-7eff-4db9-9572-401d6e1187a0
caps.latest.revision: "18"
ms.openlocfilehash: f2c928c8f61a98af3eb1e5f05881683dbcaedf1e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="send-telemetry-feedback-to-microsoft"></a>Microsoft 원격 분석 피드백 보내기
분석 플랫폼 시스템에 관리 콘솔 데이터를 Microsoft로 전송 하는 선택적 원격 분석 기능이 있습니다. 이 제품을 개선 하기 위한 필드를 사용 하는 것이 좋습니다.  
  
> [!NOTE]  
> 이 릴리스의 경우 Microsoft가 원격 분석 데이터를 적극적으로 모니터링 하지 않습니다. 데이터 분석 목적 으로만 수집 되 고 됩니다.  
  
## <a name="privacy"></a>개인 정보  
최대 개인 정보 보호를 제공 하려면 APS 원격 분석을 사용 하지 않고 제공 됩니다. 이 기능을 사용 하기 전에 먼저 검토는 [Microsoft 분석 플랫폼 시스템 개인정보취급방침](http://go.microsoft.com/fwlink/?LinkId=400902)합니다. 그런 다음 실행을 위해 옵트인 아래에 설명 된 PowerShell 스크립트입니다.  
  
## <a name="enable"></a>원격 분석을 사용 하도록 설정  
**DNS 전달:** 원격 분석 데이터를 Microsoft로 보내는 분석 플랫폼 시스템 DNS 전달자를 통해 인터넷에 연결 하는 데이 필요 합니다. 이 기능을 사용 하려면 모든 호스트 및 작업 부하 Vm에서 DNS 전달 사용 하도록 설정 해야 합니다. 호출 된 `Enable-RemoteMonitoring` 명령에 `SetupDnsForwarder` DNS 전달 구성 하 고 원격 분석을 사용 하도록 설정 하는 옵션입니다. 호출 된 `Enable-RemoteMonitoring` 없이 명령을 `SetupDnsForwarder` 옵션 DNS 전달 이미 구성 되어 있고 하트 비트 모니터링 사용 하려는 경우.  
  
> [!IMPORTANT]  
> DNS 전달을 사용 하면 모든 호스트 및 작업 부하 Vm에 대 한 인터넷 연결을 엽니다.  
  
#### <a name="to-enable-feedback"></a>피드백을 사용 하도록 설정 하려면  
  
1.  어플라이언스 도메인 관리자 계정을 사용 하 여 하는 제어 노드에 연결 (***appliance_domain*-CTL01**) 및 Windows 관리자 자격 증명을 사용 하 여 명령 프롬프트를 엽니다.  
  
2.  다음 디렉터리로 이동: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`합니다.  
  
3.  모듈 가져오기`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 사용자를 가져오려면 명령에 마침표 두 개 사용 해야 합니다.  
  
    **예:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  호출 된 `Enable-RemoteMonitoring` 명령입니다.  
  
    > [!NOTE]  
    > 스크립트에는 인터넷 연결이 제대로 작동 하 고 인터넷 연결을 확인 하지 않습니다 있다고 가정 합니다.  
  
    1.  처음으로 원격 분석을 사용 하도록 설정 하면 모든 DNS 전달자 올바르게 구성 되도록 하려면 다음 명령을 사용 합니다. 이 예제에서 DNS 전달 IP 주소를 대체 `xx.xx.xx.xx` 사용자 환경에서 DNS 전달자의 IP 주소를 사용 합니다.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  DNS 전달자를 이미 구성 하면 원격 분석을 이전에 비활성화 된 다시 사용 하도록 설정 하는 등, DNS 전달 구성 하지 않고 원격 분석을 사용 하도록 설정 하려면 다음 명령을 사용 합니다.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  읽고 APS 어플라이언스에 대 한 정보를 수집 합니다 승인할를 묻는 메시지가 나타납니다. 한 링크를 복사 하 고 검토를 위해 모든 인터넷 브라우저에 붙여 넣을 수 있는 APS 개인정보취급방침 됩니다.  
  
6.  입력 **Y** 수락 하 고 피드백에 참여 하거나 입력 **N** 을 허용 하지 않도록 합니다.  
  
7.  입력 한 경우 **Y** 는 일련의 원격 분석 (및 필요에 따라 DNS 전달자) 가능 하 게 실행 될 명령 됩니다 어플라이언스 기능입니다. 오류 또는 이동할 수는 명령이 성공 했음을 생각 되는 정보를 표시 되 면 CSS에 문의 하십시오.  
  
입력 한 경우 **N**, 명령이 없습니다 실행 되 고 기능을 사용할 수 있게 하 고 더 많은 작업을 수행할 수 없습니다.  
  
실행 하더라도 피해는는 `Enable-RemoteMonitoring` 여러 번 명령입니다. DNS 전달자 이미 설정 되어 있으면 해당 되는 경우 경고 메시지가 얻게 됩니다.  
  
## <a name="disable"></a>원격 분석을 사용 하지 않도록 설정  
원격 분석을 사용 하지 않도록 설정 하면 어플라이언스에 클라우드에서 서비스 모니터링 ap의 상태에 대 한 정보를 전달 하는 모든 작업이 중지 됩니다.  
  
> [!IMPORTANT]  
> 이 작업을 수행 DNS 전달자 또는 기기에서 다른 기능 에서도 사용 하 여에 있을 수 있는 인터넷에 연결 하지 해제 됩니다.  
  
#### <a name="to-disable-telemetry"></a>원격 분석을 사용 하지 않도록 설정 하려면  
  
1.  어플라이언스 도메인 관리자 계정을 사용 하 여 하는 제어 노드에 연결 (***appliance_domain*-CTL01**) 하 고 관리자 권한으로 PowerShell 창을 엽니다.  
  
2.  다음 디렉터리로 이동: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`합니다.  
  
3.  모듈 가져오기`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 사용자를 가져오려면 명령에 마침표 두 개 사용 해야 합니다.  
  
    **예:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  호출 된 `Disable-RemoteMonitoring` 매개 변수 없이 명령을 합니다. 이 명령은 사용자 의견 보내기 중지 됩니다. (이 영향을 주지 않습니다 로컬 모니터링 합니다.) 그러나 명령 됩니다 하지 DNS 전달자를 사용 하지 않도록 설정 및/또는 모든 인터넷 연결을 사용 하지 않도록 설정 합니다. 성공적으로 피드백을 해제 한 후 수동으로 수행 되어야 합니다.  
  
    **예:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
오류 또는 이동할 수는 명령이 성공 했음을 생각 되는 정보를 표시 되 면 CSS에 문의 하십시오.  
  
실행 하더라도 피해는는 `Disable-RemoteMonitoring` 여러 번 명령입니다.  
  
## <a name="see-also"></a>관련 항목:  
[관리 콘솔 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
[시스템 뷰 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41;](monitor-the-appliance-by-using-system-views.md)  
[System Center Operations Manager &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
[비 어플라이언스 DNS 이름 &#40;를 사용 하는 DNS 전달자 분석 플랫폼 시스템 &#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
