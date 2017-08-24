---
title: "Linux SQL Server Azure에서 VM을 프로 비전 | Microsoft Docs"
description: "이 자습서에는 Azure에서 SQL Server 2017 Linux 가상 컴퓨터를 만드는 방법을 보여 줍니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 222e23b2-51e7-429b-b8e5-61e0ebe7df9b
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 0470622b0fe5a8835213617a4fc2e8c74f674873
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-linux-sql-server-2017-virtual-machine-with-the-azure-portal"></a>Azure 포털 사용 SQL Server 2017 Linux 가상 컴퓨터 만들기

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Azure는 SQL Server 2017 RC2 설치 되어 있는 Linux 가상 컴퓨터 이미지를 제공 합니다. 이 항목에서는 Linux SQL Server 가상 컴퓨터를 만드는 Azure 포털을 사용 하는 방법에 짧은 연습을 제공 합니다. 

## <a name="create-a-linux-vm-with-sql-server-installed"></a>SQL Server가 설치 된 Linux VM 만들기

열기는 [Azure 포털](https://portal.azure.com/)합니다.

1. 클릭 **새로** 왼쪽에 있습니다.

1. 에 **새로** 블레이드에서 클릭 **계산**합니다.

1. 클릭 **모든 참조** 옆에 **을 갖춘 앱** 제목입니다.

   ![모든 VM 이미지를 참조 하십시오.](./media/sql-server-linux-azure-virtual-machine/azure-compute-blade.png)

1. 검색 상자에 입력 **SQL Server 2017**, 누릅니다 **Enter** 검색을 시작 합니다.

    ![SQL Server 2017 VM 이미지에 대 한 검색 필터](./media/sql-server-linux-azure-virtual-machine/searchfilter.png)

    > [!TIP]
    > 이 필터는 SQL Server 2017에 대 한 사용 가능한 Linux 가상 컴퓨터 이미지를 표시합니다. 시간이 지남에 따라 지원 되는 다른 Linux 배포판에 대 한 SQL Server 2017 이미지 나열 됩니다. 이 클릭할 수도 있습니다 [링크](https://ms.portal.azure.com/#blade/Microsoft_Azure_Marketplace/GalleryFeaturedMenuItemBlade/selectedMenuItemId/home/searchQuery/sql%20server%202017) SQL Server 2017에 대 한 검색 결과에 직접 이동 합니다. 

1. 검색 결과에서 SQL Server 2017 이미지를 선택 합니다.

1. **만들기**를 클릭합니다.

1. 에 **기본 사항** 블레이드에서 Linux VM에 대 한 세부 정보를 입력 합니다. 

    ![기본 사항 블레이드](./media/sql-server-linux-azure-virtual-machine/basics.png)

    > [!Note]
    > 인증을 위해 SSH 공개 키 또는 암호를 사용 하 여 선택할을 수 있습니다. SSH는 더 안전 합니다. SSH 키를 생성 하는 방법에 지침은 [만들 SSH 키는 Linux 및 Mac에서 Azure의 Linux Vm에 대 한](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-mac-create-ssh-keys)합니다. 

1. **확인**을 클릭합니다.

1. 에 **크기** 블레이드에서 컴퓨터 크기를 선택 합니다. VM 크기를 개발 및 기능 테스트에 대 한 권장 **DS2** 이상. 성능 테스트를 사용 하 여 **DS13** 이상.

    ![VM 크기를 선택 합니다.](./media/sql-server-linux-azure-virtual-machine/vmsizes.png)

    다른 크기를 보려면 선택 **모든 보기**합니다. VM 컴퓨터 크기에 대 한 자세한 내용은 참조 [Linux VM 크기](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes)합니다.

1. **선택**을 클릭합니다.

1. 에 **설정을** 블레이드에서 하거나 수 있습니다는 설정을 변경 하려면 기본 설정을 그대로 유지 합니다.

1. **확인**을 클릭합니다.

1. 에 **요약** 페이지 **확인** 여 VM을 만듭니다.

> [!NOTE]
> Azure VM은 미리 원격 연결에 대 한 SQL Server 포트 1433을 엽니다 방화벽을 구성 합니다. 하지만 원격으로 연결도 하려면 다음 섹션에 설명 된 대로 네트워크 보안 그룹 규칙을 추가 합니다.

## <a id="remote"></a>원격 연결에 대 한 구성

Azure VM에서 SQL Server에 원격으로 연결할 수 있으려면 네트워크 보안 그룹에는 인바운드 규칙을 구성 해야 합니다. SQL Server입니다 (기본값 1433)를 수신 하는 포트의 트래픽을 허용 하는 규칙입니다. 다음 단계에는이 단계에 대 한 Azure 포털을 사용 하는 방법을 보여 줍니다. 

1. 포털에서 선택 **가상 컴퓨터**, 한 다음 SQL Server VM을 선택 합니다.

1. 속성 목록에서 선택 **네트워크 인터페이스**합니다.

1. VM에 대 한 네트워크 인터페이스를 선택 합니다.

    ![네트워크 인터페이스](./media/sql-server-linux-azure-virtual-machine/networkinterfaces.png)

1. 네트워크 보안 그룹 링크를 클릭 합니다.

    ![네트워크 보안 그룹](./media/sql-server-linux-azure-virtual-machine/networksecuritygroup.png)

1. Selct 네트워크 보안 그룹의 속성에서 **인바운드 보안 규칙**합니다.

1. 클릭는 **+ 추가** 단추입니다.

1. "SQLServerRemoteConnections"의 이름을 제공 합니다.

1. 에 **서비스** 목록에서 **MS SQL**합니다.

    ![MS SQL 보안 그룹 규칙](./media/sql-server-linux-azure-virtual-machine/sqlnsgrule.png)

1. 클릭 **확인** VM에 대 한 규칙을 저장 합니다.

## <a id="connect"></a>Linux VM에 연결

이미 BASH 셸의 사용 하는 경우 사용 하 여 Azure VM에 연결 된 **ssh** 명령입니다. 다음 명령에서 VM 사용자 이름 및 IP 주소-Linux VM에 연결을 대체 합니다.

```bash
ssh -l AzureAdmin 100.55.555.555
```

Azure 포털에서 VM의 IP 주소를 찾을 수 있습니다.

![Azure 포털의 IP 주소](./media/sql-server-linux-azure-virtual-machine/vmproperties.png)

Windows에서 실행 되 고 BASH 셸의 하지 않은 경우 PuTTY 같은 SSH 클라이언트를 설치할 수 있습니다.

1. [다운로드 및 설치 PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)합니다.

1. PuTTY를 실행 합니다.

1. PuTTY 구성 화면에서 VM의 공용 IP 주소를 입력 합니다.

1. 열기를 클릭 하 고 사용자 이름 및 암호 프롬프트에를 입력 합니다.

Linux Vm에 연결 하는 방법에 대 한 자세한 내용은 참조 [포털을 사용 하 여 Azure에서 Linux VM을 만들](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-portal#ssh-to-the-vm)합니다.

## <a name="configure-sql-server"></a>SQL Server 구성

1. Linux VM에 연결한 후 새 명령을 터미널을 엽니다.

1. 다음 명령을 사용 하 여 SQL Server를 설정 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup 
   ```

   라이선스를 수락 하 고 시스템 관리자 계정에 대 한 암호를 입력 합니다. 메시지가 표시 되 면 서버를 시작할 수 있습니다.

1. 필요에 따라 [SQL Server 도구 설치](sql-server-linux-setup-tools.md)합니다.

## <a name="next-steps"></a>다음 단계

Azure에서 SQL Server 2017 가상 컴퓨터를가지고로 연결할 수 있습니다 로컬로 **sqlcmd** TRANSACT-SQL 쿼리를 실행 합니다.

SQL Server에 대 한 원격 연결에 대 한 Azure VM을 구성 해야도 원격으로 연결할 수 없습니다. Linux에서 SQL Server에 연결 하 여 원격 Windows 컴퓨터에서 예제를 보려면 [Linux에서 SQL Server에 연결 하는 Windows에서 사용 하 여 SSMS](sql-server-linux-develop-use-ssms.md)합니다.

Azure에서 Linux 가상 컴퓨터에 대 한 자세한 내용은 참조는 [Linux 가상 컴퓨터 설명서](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/)합니다.

