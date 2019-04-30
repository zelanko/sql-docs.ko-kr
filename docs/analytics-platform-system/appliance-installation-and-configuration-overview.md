---
title: 어플라이언스 설치 및 구성-Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS) 설정 하 고 새 어플라이언스를 사용 하 여 시작 하는 초기 단계 어플라이언스 단계적으로 안내 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6aa75cdab85fce9ef308d3e853ddb0107c28ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63276347"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>어플라이언스 설치 및 Analytics Platform System에 대 한 구성
Analytics Platform System (APS) 설정 하 고 새 어플라이언스를 사용 하 여 시작 하는 초기 단계 어플라이언스 단계적으로 안내 합니다.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. 하드웨어 설치  
새 어플라이언스에서 데이터 센터에서 도킹 스테이션에 책장에 전달 됩니다.  
  
> [!IMPORTANT]  
> 경우에 따라 IHV를 개봉, 랙, 및 데이터 센터에 어플라이언스를 연결 합니다. 따라서 이러한 지침 필요 하지 않습니다. 고로 건너뛸 수 있습니다는 [3입니다. 어플라이언스 구성](#ConfigureAppliance) 아래의 섹션입니다.  
  
IHV 하드웨어 설치를 수행 하지 않을 경우 하드웨어를 설치 하려면 다음 단계를 사용 합니다.  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|설명서를 확인 합니다.|모든 필요한 문서 및 정보 (IHV) 독립 하드웨어 공급 업체 로부터 받은 있는지 확인 합니다. 참조 [IHV에서 가져올 정보 &#40;Analytics Platform System&#41;](information-to-obtain-from-your-ihv.md)합니다.|  
|하드웨어 설치|데이터 센터에서 어플라이언스를 수용할 수를 확인 합니다. 데이터 센터에 어플라이언스 구성 요소를 이동 합니다. 네트워크 스위치, Pdu, 랙 및 케이블 연결 합니다. 참조 [하드웨어 설치 &#40;Analytics Platform System&#41;](hardware-installation.md)합니다.|  
  
## <a name="PowerOnAppliance"></a>2. 어플라이언스에서 전원  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|어플라이언스에서 전원|오류가 발생 하는 확인 하는 데 필요한 대기 하 여 필요한 순서 대로 각 어플라이언스 구성 요소 노드를 켭니다.|  
  
## <a name="ConfigureAppliance"></a>3. 어플라이언스 구성  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|||  
|SQL Server PDW를 사용 하 여 어플라이언스 구성**Configuration Manager**|어플라이언스 어플라이언스 암호, 표준 시간대, 네트워크 및 방화벽 설정, 보안 인증서 및 성능 및 기타 설정을 설정 하려면 Configuration Manager를 사용 합니다. 참조 [어플라이언스 구성 &#40;Analytics Platform System&#41;](appliance-configuration.md)합니다.|  
  
> [!WARNING]  
> SQL Server PDW를 사용 하 여 구성 변경 내용만 해야**Configuration Manager**합니다. 변경 내용을 통해 노출 되지 않습니다 **Configuration Manager** 지원 되지 않습니다. 예를 들어, SQL Server PDW 어플라이언스에 영어 (미국) 언어 설정을 지원합니다.  
  
## <a name="SoftwareServicing"></a>4. 소프트웨어 서비스 설정  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|SQL Server PDW 업데이트 적용|(선택 사항) 하나 이상의 SQL Server PDW 업데이트를 최신 버전 SQL Server PDW 소프트웨어 업데이트를 적용 해야 합니다. 참조 [Analytics Platform System 핫픽스 적용 &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)합니다.|  
|Windows Server Update Services 구성|소프트웨어를 지원 하기 위한 Windows Server Update Services에서 업데이트를 받는 어플라이언스를 구성 합니다. 참조 [Microsoft 업데이트 다운로드 및 적용 &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)합니다.|  
  
## <a name="NextSteps"></a>다음 단계  
이전 단계의 모든 작업을 마친 후에 어플라이언스는 사용할 수 있습니다. 수 또는 위치에서 다른 직원에 게 다음 작업을 수행할 수 있습니다.  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|SQL Server PDW 드라이버를 설치 하 고 연결 구성|SQL Server Data Tools, sqlcmd, 비즈니스 인텔리전스 소프트웨어 또는 다른 도구를 사용 하 여 SQL Server PDW에 다시 연결할 로컬 컴퓨터를 구성 합니다. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|로그온 및 서버 역할을 만들고 사용 권한을 할당합니다|계획 하 고 사용자가 적절 한 권한이 있는 SQL Server PDW에 로그온 할 수 있는 로그온 및 서버 역할을 만듭니다. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Azure 데이터 관리 게이트웨이 구성|게이트웨이 Azure 사용자를가 온-프레미스 AP 데이터 AP 데이터 보안 OData 피드를 노출 하 여 액세스할 수 있습니다. 게이트웨이 이미 제어 노드에 설치 됩니다. Microsoft 구성 사용 하 여 지원을 요청 합니다.|  
|모니터 쿼리 및 어플라이언스 사용자|쿼리 및 어플라이언스 사용자를 모니터링 하는 관리 콘솔 및 기타 리소스를 사용 합니다. 참조 [관리자 콘솔을 사용 하 여 어플라이언스 모니터링 &#40;분석 플랫폼 시스템&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|SQL Server PDW에 대 한 데이터 로드|어플라이언스에서 데이터를 로드 합니다. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|재해 복구 계획 만들기|하드웨어 오류 로부터 데이터를 보호할 방법을 계획 하거나 데이터를 덮어씁니다. 정기 백업을 사용 하는 계획을 만들고 데이터 손상 또는 손실의 경우 계획을 복원 합니다. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|어플라이언스 모니터링|시스템 뷰, 로그 및 관리 콘솔을 사용 하 여 어플라이언스 상태, 상태 및 성능을 모니터링 합니다. 수정 하거나 모든 문제를 보고 합니다. 참조 [어플라이언스 성능 상태 모니터 &#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)합니다.|  
