---
title: 원격 분석 피드백-Analytics Platform System | Microsoft Docs
description: Microsoft Analytics Platform System에 대 한 원격 분석 피드백을 보냅니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 347879cd468d67b3feee0c92dcd154334df4c237
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960090"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Analytics Platform System에 대 한 Microsoft 원격 분석 피드백 보내기
Analytics Platform System에 microsoft 관리 콘솔 데이터를 전송 하는 선택적 원격 분석 기능이 있습니다. 
  
> [!NOTE]  
> 이 릴리스에서 Microsoft가 원격 분석 데이터를 적극적으로 모니터링 하지 않습니다. 분석 목적 으로만 수집 중인 데이터  
  
## <a name="privacy"></a>개인 정보  
최대 개인 정보 보호를 제공 하려면 AP는 원격 분석을 사용 하지 않고 제공 됩니다. 이 기능을 사용 하기 전에 먼저 검토 합니다 [Microsoft Analytics Platform System 개인정보취급방침](https://go.microsoft.com/fwlink/?LinkId=400902)합니다. 옵트인 하려면 아래 설명 된 PowerShell 스크립트를 실행 합니다.  
  
## <a name="enable"></a>원격 분석을 사용 하도록 설정  
**DNS 전달 합니다.** Microsoft로 원격 분석 데이터를 보내는 DNS 전달자를 통해 인터넷에 연결할 Analytics Platform System 필요 합니다. 이 기능을 사용 하려면 모든 호스트 및 Vm 워크 로드에 전달 하는 DNS를 설정 해야 합니다. 호출을 `Enable-RemoteMonitoring` 명령과 `SetupDnsForwarder` 제대로 DNS 전달을 구성 하 고 원격 분석을 사용 하도록 설정 하는 옵션입니다. 호출을 `Enable-RemoteMonitoring` 없이 명령을 합니다 `SetupDnsForwarder` DNS 전달을 이미 구성 되어 있고 하트 비트 모니터링 사용 하려는 경우 옵션입니다.  
  
> [!IMPORTANT]  
> DNS 전달을 사용 하도록 설정 하면 모든 호스트 및 워크 로드 Vm에 대 한 인터넷 연결이 열립니다.  
  
#### <a name="to-enable-feedback"></a>피드백을 사용 하도록 설정 하려면  
  
1.  어플라이언스 도메인 관리자 계정으로 사용 하 여 제어 노드에 연결 (<strong>*appliance_domain*-CTL01</strong>) Windows 관리자 자격 증명을 사용 하 여 명령 프롬프트를 엽니다.  
  
2.  다음 디렉터리로 이동 합니다. `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`합니다.  
  
3.  모듈 가져오기 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 가져올를 명령에는 마침표 두 개 사용 해야 합니다.  
  
    **예제:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  호출 된 `Enable-RemoteMonitoring` 명령입니다.  
  
    > [!NOTE]  
    > 스크립트에는 인터넷 연결이 제대로 작동 하는 인터넷 연결을 확인 하지 않습니다 있다고 가정 합니다.  
  
    1.  처음으로 원격 분석을 사용 하도록 설정 하면 모든 DNS 전달자 올바르게 구성 되었는지 확인 하려면 다음 명령을 사용 합니다. 이 예제의 DNS 전달 된 IP 주소를 바꿉니다 `xx.xx.xx.xx` 환경의 DNS 전달자의 IP 주소를 사용 하 여 합니다.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  DNS 전달자를 이미 구성 하면 원격 분석을 이전에 비활성화 다시 사용 하도록 설정 하는 등, DNS 전달을 구성 하지 않고 원격 분석을 사용 하도록 설정 하려면 다음 명령을 사용 합니다.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  읽기 및 APS가 어플라이언스에 대 한 정보를 수집할 것임을 확인 하 라는 메시지가 표시 됩니다. 복사 및 검토를 위해 인터넷 브라우저에 붙여 넣을 수 있는 APS 개인정보취급방침 연결이 됩니다.  
  
6.  입력 **Y** 수락 및 의견 옵트인 하거나 입력 **N** 동의 하지 않았습니다.  
  
7.  입력 한 경우 **Y** 일련의 원격 분석 (및 필요에 따라 DNS 전달자) 가능 하 게 실행 될 명령 됩니다 어플라이언스 기능입니다. 모든 오류 또는 명령이 성공한 생각 하는 정보를 표시 하는 경우 CSS에 문의.  
  
입력 한 경우 **N**에서는 어떤 명령도 실행 되는 기능을 사용할 수 없습니다 및 아무 작업도 수행할 수 없습니다.  
  
실행에서 아무런 문제가 없습니다를 `Enable-RemoteMonitoring` 여러 번 명령입니다. DNS 전달자 이미 설정 되어 있으면이 나타내는 경고 메시지가 표시 됩니다.  
  
## <a name="disable"></a>원격 분석을 사용 하지 않도록 설정  
원격 분석을 사용 하지 않도록 설정 하면 클라우드 서비스 모니터링 AP에 어플라이언스의 상태에 대 한 정보를 통신 하는 모든 작업이 중지 됩니다.  
  
> [!IMPORTANT]  
> 이 작업을 수행 하면 DNS 전달자 또는 어플라이언스의 다른 기능에서 사용할 수 있는 인터넷 연결 비활성화 되지는 않습니다.  
  
#### <a name="to-disable-telemetry"></a>원격 분석을 사용 하지 않도록 설정  
  
1.  어플라이언스 도메인 관리자 계정으로 사용 하 여 제어 노드에 연결 (<strong>*appliance_domain*-CTL01</strong>) 하 고 관리자 권한으로 PowerShell 창을 엽니다.  
  
2.  다음 디렉터리로 이동 합니다. `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`합니다.  
  
3.  모듈 가져오기 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 가져올를 명령에는 마침표 두 개 사용 해야 합니다.  
  
    **예제:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  호출 된 `Disable-RemoteMonitoring` 매개 변수 없이 명령을 합니다. 이 명령은 사용자 의견 보내기 중지 됩니다. (이 영향을 주지 않습니다 로컬 모니터링 합니다.) 그러나 명령이 됩니다 하지 DNS 전달자를 사용 하지 않도록 설정 하거나 모든 인터넷 연결을 사용 하지 않도록 설정 합니다. 이 성공적으로 피드백을 해제 한 후 수동으로 수행 되어야 합니다.  
  
    **예제:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
모든 오류 또는 명령이 성공한 생각 하는 정보를 표시 하는 경우 CSS에 문의.  
  
실행에서 아무런 문제가 없습니다를 `Disable-RemoteMonitoring` 여러 번 명령입니다.  
  
## <a name="next-steps"></a>다음 단계
참조 항목:
- [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [시스템 뷰를 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [System Center Operations Manager를 사용 하 여 어플라이언스 모니터링 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [DNS 전달자를 사용 하 여 비 어플라이언스 DNS 이름을 확인 하려면 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
