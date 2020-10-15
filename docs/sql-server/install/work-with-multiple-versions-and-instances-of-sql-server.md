---
title: 여러 버전 및 인스턴스 작업
description: SQL Server를 여러 개 설치하거나 이전 SQL Server 버전이 이미 설치되어 있는 컴퓨터에 SQL Server를 설치할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- concurrent installations [SQL Server]
- versions [SQL Server], multiple
- side-by-side installations [SQL Server]
- multiple SQL Server component versions
- installing SQL Server, side-by-side installations
- Setup [SQL Server], side-by-side installations
- 64-bit edition [SQL Server]
- 32-bit edition [SQL Server]
- editions [SQL Server], side-by-side installations
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a2f9c1f0a6f73d4f2e2dfa5556548d3e1d5d9481
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988099"
---
# <a name="work-with-multiple-versions-and-instances-of-sql-server"></a>여러 버전 및 인스턴스의 SQL Server 작업

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

SQL Server를 여러 개 설치하거나 이전 SQL Server 버전이 이미 설치되어 있는 컴퓨터에 SQL Server를 설치할 수 있습니다.

다음 SQL Server 관련 항목은 동일한 컴퓨터에 여러 개를 설치한 경우에도 작동합니다.

- 데이터베이스 엔진

- Analysis Services

- Reporting Services(SQL Server 2016 및 이전) SQL Server 2016부터 SSRS(SQL Server Reporting Services)에는 별도의 설치가 있습니다. 


다른 SQL Server 버전이 이미 설치되어 있는 컴퓨터에서 이전 버전의 SQL Server를 업그레이드할 수 있습니다. 지원되는 업그레이드 시나리오에 대한 자세한 내용은 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)를 참조하세요.
  
## <a name="version-components-and-numbering"></a>버전 구성 요소 및 번호 지정

 다음 개념은 두 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 함께 설치된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동작을 이해하는 데 유용합니다.
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 표준 제품 버전 형식은 MM.nn.bbbb.rr입니다. 여기서 각 세그먼트는 다음과 같이 정의됩니다.
  
 MM - 주 버전  
  
 nn - 부 버전  
  
 bbbb - 빌드 번호  
  
 rr - 빌드 수정 번호  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 주 버전 또는 부 버전이 릴리스될 때마다 이전 버전과의 차별성을 위해 버전 번호가 증가합니다. 이러한 버전 변경은 다양한 용도로 사용됩니다. 사용자 인터페이스에 버전 정보 표시, 업그레이드하는 동안 파일 대체 방식 제어, 서비스 팩 적용, 연속 버전 간의 기능적 차이를 위한 메커니즘 등을 예로 들 수 있습니다.
  
### <a name="components-shared-by-all-versions-of-ssnoversion"></a>모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

 특정 구성 요소는 설치된 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전의 모든 인스턴스에서 공유합니다. 이러한 구성 요소는 버전이 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 같은 컴퓨터에 함께 설치하면 자동으로 최신 버전으로 업그레이드됩니다. 일반적으로 이러한 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 마지막 인스턴스가 제거되면 자동으로 제거됩니다.
  
 예제: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 및 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS 기록기.
  
### <a name="components-shared-across-all-instances-of-the-same-major-version-of-ssnoversion"></a>주 버전이 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 모든 인스턴스는 일부 구성 요소를 공유합니다. 업그레이드 중에 공유 구성 요소가 선택되면 기존 구성 요소가 최신 버전으로 업그레이드됩니다.
  
예제: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서
  
### <a name="components-shared-across-minor-versions"></a>부 버전에서 공유하는 구성 요소

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 공유하는 구성 요소입니다.
  
예제: 설치 지원 파일.
  
### <a name="components-specific-to-an-instance-of-ssnoversion"></a>다음의 특정 인스턴스에 고유한 구성 요소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 또는 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 인스턴스에 고유합니다. 이를 인스턴스 인식 구성 요소 또는 서비스라고도 합니다. 인스턴스 인식 구성 요소 또는 서비스는 자신을 호스팅하는 인스턴스와 같은 버전을 공유하고 해당 인스턴스에만 독점적으로 사용됩니다.
  
예제: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
### <a name="components-that-are-independent-of-the-ssnoversion-versions"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 독립적인 구성 요소

특정 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치할 때 설치되지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전과 관계가 없습니다. 이러한 구성 요소는 주 버전 간에 공유될 수도 있고 모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 공유될 수도 있습니다.  

예제: Microsoft Sync Framework, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 설치에 대한 자세한 내용은 [설치 마법사에서 SQL Server 2016 설치&#40;설치 프로그램&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact를 제거하는 방법은 [SQL Server의 기존 인스턴스 제거&#40;설치 프로그램&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)를 참조하세요.  
  
## <a name="using-ssnoversion-side-by-side-with-previous-versions-of-ssnoversion"></a>이전 버전과 함께 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 다음을 함께 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 인스턴스가 이미 실행 중인 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치할 수 있습니다. 컴퓨터에 기본 인스턴스가 이미 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 명명된 인스턴스로 설치되어야 합니다.  

다음 표에서는 .NET의 필수 버전이 설치되어 있는 일반적으로 지원되는 Windows의 버전에서 SQL Server의 각 버전에 대한 side-by-side 지원을 보여 줍니다.

| 기존 인스턴스 | Side by side 지원| 
|-------------------|----------------------------|
| SQL Server 2019 | SQL Server 2008 ~ SQL Server 2017| 
| SQL Server 2017 | SQL Server 2008 ~ SQL Server 2016| 
| SQL Server 2016 | SQL Server 2008 ~ SQL Server 2014| 

자세한 내용은 [Windows 8 이상에서 SQL Server 사용](https://support.microsoft.com/help/2681562/using-sql-server-in-windows-8-and-later-versions-of-windows-operating)을 참조하세요. 

  
> [!CAUTION]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 준비 인스턴스를 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같은 컴퓨터에 함께 설치할 수 없습니다. 예를 들어 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 준비 인스턴스와 함께 준비할 수 없습니다. 그러나 같은 주 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 준비 인스턴스를 같은 컴퓨터에 여러 개 설치할 수 있습니다. 자세한 내용은 [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)을 참조하세요.  
>
> SQL Server 2016 이상은 Windows Server 2008 R2 Server Core SP1을 실행하는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전과 함께 side-by-side 설치할 수 없습니다. Server Core 설치에 대한 자세한 내용은 [Server Core에 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-on-server-core.md)를 참조하세요.  
  


## <a name="preventing-ip-address-conflicts"></a>IP 주소 충돌 방지

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스가 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 독립 실행형 인스턴스와 함께 설치되는 경우 IP 주소의 TCP 포트 번호가 충돌하지 않도록 주의합니다. 일반적으로 충돌은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 두 인스턴스가 모두 기본 TCP 포트(1433)를 사용하도록 구성되는 경우 발생합니다. 충돌을 방지하려면 한 인스턴스가 기본이 아닌 고정 포트를 사용하도록 구성합니다. 고정 포트는 일반적으로 독립 실행형 인스턴스에서 더 쉽게 구성할 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 다른 포트를 사용하도록 구성하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스가 실패하여 대기 노드가 될 때 인스턴스 시작을 차단하는 예기치 않은 IP 주소/TCP 포트 충돌이 방지됩니다.
  
## <a name="see-also"></a>참고 항목

* [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
* [설치 마법사에서 SQL Server 설치 &#40;Setup&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
* [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)
* [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)
* [버전 및 SQL Server 2017 의 지원 되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)
* [버전 및 SQL Server 2016 의 지원 되는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md)
* [이전 버전과의 호환성_삭제됨](/previous-versions/sql/sql-server-2016/cc280407(v=sql.130))