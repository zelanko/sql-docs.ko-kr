---
title: 어플라이언스 설치 및 구성
description: 새 어플라이언스를 설정 하 고 시작 하는 초기 단계를 통해 분석 플랫폼 시스템 (AP) 어플라이언스 관리자를 안내 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9f96d953dbd427bfb6cf94470c0ee80ade3aed48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401442"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>분석 플랫폼 시스템에 대 한 어플라이언스 설치 및 구성
새 어플라이언스를 설정 하 고 시작 하는 초기 단계를 통해 분석 플랫폼 시스템 (AP) 어플라이언스 관리자를 안내 합니다.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="1-install-the-hardware"></a><a name="InstallHardware"></a>1. 하드웨어 설치  
새 어플라이언스는 pallets에서 데이터 센터의 도크로 배달 됩니다.  
  
> [!IMPORTANT]  
> 경우에 따라 IHV는 데이터 센터에서 어플라이언스를 압축 하 고, 랙에 연결 하 고, 연결 합니다. 이 경우에는 이러한 지침이 필요 하지 않으며 3으로 건너뛸 수 있습니다 [. 아래에서 어플라이언스 섹션을 구성](#ConfigureAppliance) 합니다.  
  
IHV가 하드웨어 설치를 수행 하지 않는 경우 다음 단계를 사용 하 여 하드웨어를 설치 합니다.  
  
|||  
|-|-|  
|**Task**|**설명**|  
|설명서 확인|독립 하드웨어 공급 업체 (IHV)에서 필요한 모든 문서와 정보를 받았는지 확인 합니다. [IHV &#40;분석 플랫폼 시스템&#41;에서 얻을 수 있는 정보 ](information-to-obtain-from-your-ihv.md)를 참조 하세요.|  
|하드웨어 설치|데이터 센터가 어플라이언스를 수용할 수 있는지 확인 합니다. 어플라이언스 구성 요소를 데이터 센터로 이동 합니다. 네트워크 스위치, Pdu 및 케이블을 랙에 연결 합니다. [하드웨어 설치 &#40;분석 플랫폼 시스템&#41;](hardware-installation.md)을 참조 하세요.|  
  
## <a name="2-power-on-the-appliance"></a><a name="PowerOnAppliance"></a>2. 어플라이언스 전원 켜기  
  
|||  
|-|-|  
|**Task**|**설명**|  
|어플라이언스의 전원 켜기|필요한 순서로 각 어플라이언스 구성 요소 노드의 전원을 켜고 오류가 발생 하지 않았는지 확인 하기 위해 필요에 따라 대기 합니다.|  
  
## <a name="3-configure-the-appliance"></a><a name="ConfigureAppliance"></a>3. 어플라이언스 구성  
  
|||  
|-|-|  
|**Task**|**설명**|  
|||  
|SQL Server PDW를 사용 하 여 어플라이언스를 구성**Configuration Manager**|어플라이언스에 대 한 어플라이언스 암호, 표준 시간대, 네트워크 및 방화벽 설정, 보안 인증서, 성능 및 기타 설정을 설정 하려면 Configuration Manager을 사용 합니다. [어플라이언스 구성 &#40;분석 플랫폼 시스템&#41;](appliance-configuration.md)을 참조 하세요.|  
  
> [!WARNING]  
> 구성 변경은 SQL Server PDW**Configuration Manager**사용 해야만 이루어져야 합니다. **Configuration Manager** 를 통해 노출 되지 않는 변경은 지원 되지 않습니다. 예를 들어 SQL Server PDW 어플라이언스는 미국 영어 설정만 지원 합니다.  
  
## <a name="4-set-up-software-servicing"></a><a name="SoftwareServicing"></a>4. 소프트웨어 서비스 설정  
  
|||  
|-|-|  
|**Task**|**설명**|  
|SQL Server PDW 업데이트 적용|필드 SQL Server PDW 소프트웨어를 최신 버전으로 업데이트 하려면 하나 이상의 SQL Server PDW 업데이트를 적용 해야 할 수 있습니다. Analytics [Platform System 핫픽스 &#40;Analytics Platform system&#41;적용 ](apply-analytics-platform-system-hotfixes.md)을 참조 하세요.|  
|Windows Server Update Services 구성|지원 소프트웨어에 대 한 Windows Server Update Services의 업데이트를 받도록 어플라이언스를 구성 합니다. [Microsoft 업데이트 다운로드 및 적용 &#40;분석 플랫폼 시스템&#41;](download-and-apply-microsoft-updates.md)을 참조 하세요.|  
  
## <a name="next-steps"></a><a name="NextSteps"></a>다음 단계  
위의 단계를 모두 완료 한 후에는 어플라이언스를 사용할 준비가 된 것입니다. 사용자 또는 해당 위치에 있는 다른 직원은 다음 작업을 진행할 수 있습니다.  
  
|||  
|-|-|  
|**Task**|**설명**|  
|SQL Server PDW 드라이버 설치 및 연결 구성|SQL Server Data Tools, sqlcmd, 비즈니스 인텔리전스 소프트웨어 또는 기타 도구를 사용 하 여 SQL Server PDW에 연결 하도록 로컬 컴퓨터를 구성 합니다. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|로그온 및 서버 역할을 만들고 사용 권한을 할당 합니다.|사용자가 적절 한 사용 권한으로 SQL Server PDW에 로그온 할 수 있도록 허용 하는 로그온 및 서버 역할을 계획 하 고 만듭니다. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Azure 데이터 관리 게이트웨이 구성|게이트웨이를 통해 Azure 사용자는 AP 데이터를 보안 OData 피드로 노출 하 여 온-프레미스 AP 데이터에 액세스할 수 있습니다. 게이트웨이가 제어 노드에 이미 설치 되어 있습니다. 구성에 대 한 도움이 필요 하면 Microsoft에 문의 하세요.|  
|쿼리 및 어플라이언스 사용자 모니터링|관리 콘솔과 기타 리소스를 사용 하 여 쿼리 및 어플라이언스 사용자를 모니터링 합니다. [관리 콘솔 &#40;분석 플랫폼 시스템을 사용 하 여 어플라이언스 모니터링](monitor-the-appliance-by-using-the-admin-console.md) 을 참조 하세요&#41;<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|SQL Server PDW에 데이터 로드|데이터를 어플라이언스로 로드 합니다. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|재해 복구 계획 만들기|하드웨어 오류 또는 데이터 덮어쓰기 로부터 데이터를 보호 하는 방법을 계획 합니다. 데이터 손상이 나 손실의 경우 정기적인 백업 및 복원 계획을 사용 하 여 계획을 만듭니다. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|어플라이언스 모니터링|시스템 뷰, 로그 및 관리 콘솔을 사용 하 여 어플라이언스 상태, 상태 및 성능을 모니터링 합니다. 문제를 수정 하거나 문제를 보고 하십시오. [모니터 어플라이언스 상태 &#40;분석 플랫폼 시스템&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)을 참조 하세요.|  
