---
title: "클라우드의 SQL Server 2017 시작 | Microsoft Docs"
description: "이 빠른 시작 자습서에는 SQL Server 2017 linux 원하는 클라우드에서 실행 하는 방법을 보여 줍니다."
author: annashres
ms.author: annashres
manager: jhubbard
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.openlocfilehash: 0bc304b50930f8c8de5d244ea0b606add5f24d2f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="run-the-sql-server-2017-in-the-cloud"></a>SQL Server 2017은 클라우드에서 실행

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 빠른 시작 자습서에서는 Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES), 또는 사용자가 선택한 클라우드에 Ubuntu에 SQL Server 2017을 설치 합니다. 로 이동 [Azure 포털에서 Linux SQL Server 가상 컴퓨터를 프로 비전](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) Azure에서 Linux에서 SQL Server를 실행 합니다.

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Amazon 웹 서비스
1.  Linux a m I 3.25 g B 이상의 시장에서 메모리를 사용 하 여 만들기 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  에 연결 된 a m I s s h
1.  선택한 Linux distrbution에 대 한 빠른 시작을 수행 합니다. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  원격 연결에 대해 구성 합니다. 
    * 열기는 [Amazon EC2 콘솔]( https://console.aws.amazon.com/ec2/)
    * 탐색 창에서 선택 **보안 그룹**합니다. 
    * 선택 **인바운드, Edit, 규칙 추가**
    * SQL Server (기본 TCP 포트 (1433)는 수신 포트의 트래픽을 허용 하는 인바운드 규칙 추가

    
## <a name="digital-ocean"></a>디지털 Ocean
1. 로그인에는 [제어판](https://cloud.digitalocean.com/login) 드롭릿 만들기 클릭
1. Ubuntu 16.04 드롭릿 3.25 g b 이상 메모리를 선택 합니다.
1. 에 연결 된 드롭릿 ssh
1. 수행 된 [Ubuntu 퀵 스타트](quickstart-install-connect-ubuntu.md)
1. 원격 연결에 대해 구성 합니다.
    * 제어판의 위쪽에 따라는 **네트워킹** 링크를 클릭 한 **방화벽**
    * SQL Server (기본 TCP 포트 (1433)는 수신 포트의 트래픽을 허용 하는 인바운드 규칙 추가
    
## <a name="google-cloud-platform"></a>Google 클라우드 플랫폼
1.  3.25 g B 이상의 클라우드 실행 프로그램의 메모리와 Linux 이미지를 만들려면 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  이미지에 연결 된 ssh
1.  선택한 Linux distrbution에 대 한 빠른 시작을 수행 합니다. 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  원격 연결에 대해 구성 합니다. 
    * 이동 하 여 [방화벽 규칙](https://console.cloud.google.com/networking/firewalls)
    * SQL Server (기본 tcp: 1433)는 수신 포트의 트래픽을 허용 하는 인바운드 규칙 추가
