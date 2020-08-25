---
title: 원격 분석 피드백
description: 분석 플랫폼 시스템에 대 한 원격 분석 피드백을 Microsoft에 보냅니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400361"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 원격 분석 피드백을 Microsoft에 보내기
분석 플랫폼 시스템에는 관리 콘솔 데이터를 Microsoft로 보내는 선택적 원격 분석 기능이 있습니다. 
  
> [!NOTE]  
> 이 릴리스에서 Microsoft는 원격 분석 데이터를 적극적으로 모니터링 하 고 있지 않습니다. 데이터는 분석 목적 으로만 수집 됩니다.  
  
## <a name="privacy"></a><a name="privacy"></a>개인 정보 취급 방침  
최대 개인 정보 보호를 제공 하기 위해 AP는 원격 분석을 사용 하지 않고 제공 됩니다. 이 기능을 사용 하도록 설정 하기 전에 먼저 [Microsoft Analytics Platform System 개인 정보 취급 방침](https://go.microsoft.com/fwlink/?LinkId=400902)을 검토 합니다. 옵트인 하려면 아래 설명 된 PowerShell 스크립트를 실행 합니다.  
  
## <a name="enable-telemetry"></a><a name="enable"></a>원격 분석 사용  
**DNS 전달:** Microsoft로 원격 분석 데이터를 전송 하려면 분석 플랫폼 시스템에서 DNS 전달자를 통해 인터넷에 연결 해야 합니다. 이 기능을 사용 하도록 설정 하려면 모든 호스트 및 워크 로드 Vm에서 DNS 전달을 사용 하도록 설정 해야 합니다. `Enable-RemoteMonitoring` `SetupDnsForwarder` DNS 전달을 적절히 구성 하 고 원격 분석을 사용 하도록 설정 하는 옵션을 사용 하 여 명령을 호출 합니다. `Enable-RemoteMonitoring` `SetupDnsForwarder` DNS 전달이 이미 구성 되어 있고 하트 비트 모니터링만 사용 하도록 설정 하려는 경우 옵션을 사용 하지 않고 명령을 호출 합니다.  
  
> [!IMPORTANT]  
> DNS 전달을 사용 하도록 설정 하면 모든 호스트 및 워크 로드 Vm에 대 한 인터넷 연결이 열립니다.  
  
#### <a name="to-enable-feedback"></a>피드백을 사용 하도록 설정 하려면  
  
1.  어플라이언스 도메인 관리자 계정을 사용 하 여 제어 노드<strong>*appliance_domain*(CTL01</strong>)에 연결 하 고 Windows 관리자 자격 증명을 사용 하 여 명령 프롬프트를 엽니다.  
  
2.  다음 디렉터리로 이동 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 합니다.  
  
3.  모듈 가져오기 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 가져오려면 명령에서 두 개의 마침표를 사용 해야 합니다.  
  
    **예:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  명령을 호출 `Enable-RemoteMonitoring` 합니다.  
  
    > [!NOTE]  
    > 이 스크립트에서는 인터넷 연결이 제대로 작동 하 고 인터넷 연결의 유효성을 검사 하지 않는 것으로 가정 합니다.  
  
    1.  처음으로 원격 분석을 사용 하도록 설정 하는 경우 다음 명령을 사용 하 여 모든 DNS 전달 자가 올바르게 구성 되었는지 확인 합니다. 이 예제에서는 DNS 전달 된 IP 주소를 `xx.xx.xx.xx` 사용자 환경의 Dns 전달자 ip 주소로 바꿉니다.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  이전에 사용 하지 않도록 설정 된 원격 분석을 다시 사용 하도록 설정 하는 등 DNS 전달자를 이미 구성한 경우에는 다음 명령을 사용 하 여 DNS 전달을 구성 하지 않고 원격 분석을 사용  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  AP가 어플라이언스에 대 한 정보를 수집 한다는 것을 읽고 승인 하 라는 메시지가 표시 됩니다. 검토를 위해 모든 인터넷 브라우저에 복사 하 여 붙여 넣을 수 있는 APS 개인 정보 취급 방침에 대 한 링크가 있습니다.  
  
6.  사용자 의견을 수락 하 고 옵트인 하려면 **Y** 를 입력 하 고 수락 하지 않으려면 **N** 을 입력 합니다.  
  
7.  **Y** 를 입력 한 경우 어플라이언스에서 원격 분석 (및 필요에 따라 DNS 전달자) 기능을 사용 하도록 설정 하는 일련의 명령이 실행 됩니다. 명령이 성공적으로 실행 되지 않는다고 생각 되는 오류 또는 정보가 표시 되 면 CSS에 문의 하 여 도움을 요청 합니다.  
  
**N**을 입력 한 경우에는 명령이 실행 되지 않으며 기능이 사용 하도록 설정 되지 않으며 더 이상 수행할 작업이 없습니다.  
  
명령을 여러 번 실행 하는 경우에는 나쁜 영향을 주지 않습니다 `Enable-RemoteMonitoring` . DNS 전달 자가 이미 설정 된 경우에 대 한 경고 메시지가 표시 됩니다.  
  
## <a name="disable-telemetry"></a><a name="disable"></a>원격 분석 사용 안 함  
원격 분석을 사용 하지 않도록 설정 하면 클라우드의 AP 모니터링 서비스에 대 한 어플라이언스 상태 정보를 전달 하는 모든 작업이 중지 됩니다.  
  
> [!IMPORTANT]  
> 이 작업을 수행 해도 기기의 다른 기능에서 사용 중일 수 있는 DNS 전달자 또는 인터넷 연결을 사용 하지 않도록 설정 하지 않습니다.  
  
#### <a name="to-disable-telemetry"></a>원격 분석을 사용 하지 않도록 설정 하려면  
  
1.  어플라이언스 도메인 관리자 계정을 사용 하 여 제어 노드<strong>*appliance_domain*(CTL01</strong>)에 연결 하 고 관리자 권한으로 PowerShell 창을 엽니다.  
  
2.  다음 디렉터리로 이동 `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100` 합니다.  
  
3.  모듈 가져오기 `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > 가져오려면 명령에서 두 개의 마침표를 사용 해야 합니다.  
  
    **예:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  `Disable-RemoteMonitoring`매개 변수 없이 명령을 호출 합니다. 이 명령은 사용자 의견 전송을 중지 합니다. 로컬 모니터링에는 영향을 주지 않습니다. 그러나이 명령은 DNS 전달자를 사용 하지 않도록 설정 하거나 인터넷 연결을 사용 하지 않도록 설정 하지 않습니다. 사용자 의견을 사용 하지 않도록 설정한 후 수동으로 수행 해야 합니다.  
  
    **예:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
명령이 성공적으로 실행 되지 않는다고 생각 되는 오류 또는 정보가 표시 되 면 CSS에 문의 하 여 도움을 요청 합니다.  
  
명령을 여러 번 실행 하는 경우에는 나쁜 영향을 주지 않습니다 `Disable-RemoteMonitoring` .  
  
## <a name="next-steps"></a>다음 단계
자세한 내용은 다음을 참조하세요.
- [관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [시스템 뷰 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-system-views.md)  
- [System Center Operations Manager &#40;Analytics Platform System을 사용 하 여 어플라이언스를 모니터링&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [DNS 전달자를 사용 하 여 &#40;분석 플랫폼 시스템을 사용 하 여 비 어플라이언스 DNS 이름을 확인&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
