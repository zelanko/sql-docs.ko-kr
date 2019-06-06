---
title: 클라우드에서 (Linux)의 SQL Server 시작
titleSuffix: SQL Server
description: 이 빠른 시작에는 선택한 클라우드에서 Linux의 SQL Server를 실행 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 10/25/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 3530436b08ae05e6e10a42720b47688f50077a27
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713553"
---
# <a name="quickstart-run-sql-server-in-the-cloud"></a>빠른 시작: 클라우드에서 SQL Server를 실행 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 빠른 시작에서는 Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server SLES () 또는 사용자가 선택한 클라우드에 Ubuntu에서 SQL Server를 설치 합니다. 로 이동 [Azure portal에서 Linux SQL Server 가상 컴퓨터를 프로 비전](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json) Azure에서 Linux 기반 SQL Server를 실행 합니다.

> [!NOTE]
> 유료 버전의 SQL Server를 실행 하려는 경우 사용자 고유의 라이선스 필요 (BYOL) 해야 합니다.

## <a name="amazon-web-services"></a>Amazon Web Services
1.  최소 2GB의 marketplace에서 메모리를 사용 하 여 Linux AMI 만들기 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Ssh를 사용 하 여 AMI에 연결
1.  선택한 Linux 배포에 대 한 빠른 시작을 수행 합니다. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  원격 연결에 대해 구성 합니다. 
    * 열기는 [Amazon EC2 콘솔]( https://console.aws.amazon.com/ec2/)
    * 탐색 창에서 선택 **보안 그룹**합니다. 
    * 선택 **인바운드, 편집, 규칙 추가**
    * SQL Server (기본 TCP 포트 1433)를 수신 하는 포트에서 트래픽을 허용 하도록 인바운드 규칙 추가

    
## <a name="digital-ocean"></a>Digital Ocean
1. 에 로그인 합니다 [제어판](https://cloud.digitalocean.com/login) 드롭릿 만들기 클릭
1. 최소 2GB의 메모리를 사용 하 여 Ubuntu 16.04 드롭릿을 선택 합니다.
1. Ssh를 사용 하 여 드롭릿에 연결
1. 수행 된 [Ubuntu 빠른 시작](quickstart-install-connect-ubuntu.md)
1. 원격 연결에 대해 구성 합니다.
    * 제어판의 맨 위에 있는 수행 합니다 **네트워킹** 링크를 선택한 **방화벽**
    * SQL Server (기본 TCP 포트 1433)를 수신 하는 포트에서 트래픽을 허용 하도록 인바운드 규칙 추가
    
## <a name="google-cloud-platform"></a>Google Cloud Platform
1.  최소 2GB의 클라우드 시작 관리자에서 메모리를 사용 하 여 Linux 이미지를 만들려면 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Ssh를 사용 하 여 이미지에 연결
1.  선택한 Linux 배포에 대 한 빠른 시작을 수행 합니다. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  원격 연결에 대해 구성 합니다. 
    * 로 이동 합니다 [방화벽 규칙](https://console.cloud.google.com/networking/firewalls)
    * SQL Server는 수신 포트에서 트래픽을 허용 하도록 인바운드 규칙을 추가 (기본 tcp: 1433)
