---
title: 클라우드에서 SQL Server on Linux 시작
titleSuffix: SQL Server
description: 선택한 클라우드의 RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 또는 Ubuntu에서 SQL Server를 설치하는 방법을 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: d40072ea8b347001feba5d74e6e08c8c4c8ae340
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88089033"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>빠른 시작: 클라우드에서 SQL Server 실행
[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 빠른 시작에서는 선택한 클라우드에서 RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 또는 Ubuntu에 SQL Server를 설치합니다. [Azure Portal 에서 Linux SQL Server 가상 머신 프로비저닝](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)으로 이동하여 Azure에서 SQL Server on Linux를 실행합니다.

> [!NOTE]
> 유료 버전의 SQL Server를 실행하도록 선택하면 사용자 라이선스가 필요합니다(BYOL).

## <a name="amazon-web-services"></a>Amazon Web Services
1.  마켓플레이스에서 최소 2GB의 메모리로 Linux AMI 만들기 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2+](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  SSH를 사용하여 AMI에 연결
1.  선택한 Linux 배포에 대한 빠른 시작을 따릅니다. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  원격 연결용으로 구성합니다. 
    * [Amazon EC2 콘솔]( https://console.aws.amazon.com/ec2/)을 엽니다.
    * 탐색 창에서 **보안 그룹**을 선택합니다. 
    * **인바운드, 편집, 규칙 추가**를 선택합니다.
    * SQL Server가 수신 대기하는 포트에서 트래픽을 허용하는 인바운드 규칙을 추가합니다(기본 TCP 포트 1433).

    
## <a name="digital-ocean"></a>Digital Ocean
1. [제어판](https://cloud.digitalocean.com/login)에 로그인하여 droplet 만들기를 클릭합니다.
1. 최소 2GB의 메모리를 사용하여 Ubuntu 16.04 droplet을 선택합니다.
1. SSH를 사용하여 droplet에 연결
1. [Ubuntu 빠른 시작](quickstart-install-connect-ubuntu.md)을 따릅니다.
1. 원격 연결용으로 구성합니다.
    * 제어판의 위쪽에서 **네트워킹** 링크를 따라 이동한 후 **방화벽**을 선택합니다.
    * SQL Server가 수신 대기하는 포트에서 트래픽을 허용하는 인바운드 규칙을 추가합니다(기본 TCP 포트 1433).
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  Cloud Launcher에서 최소 2GB의 메모리로 Linux 이미지 만들기 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP4](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  SSH를 사용하여 이미지에 연결
1.  선택한 Linux 배포에 대한 빠른 시작을 따릅니다. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  원격 연결용으로 구성합니다. 
    * [방화벽 규칙](https://console.cloud.google.com/networking/firewalls)으로 이동합니다.
    * SQL Server가 수신 대기하는 포트에서 트래픽을 허용하는 인바운드 규칙을 추가합니다(기본 TCP: 1433).
