---
title: "어플라이언스에 설치 및 구성 개요 (분석 플랫폼 시스템)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10934f62-4acf-4ca5-b550-f426ba81fe11
caps.latest.revision: "23"
ms.openlocfilehash: 719447d2f6d9376ec9db35f35c7f38b50ef460fa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="appliance-installation-and-configuration-overview"></a>어플라이언스에 설치 및 구성 개요
초기 단계를 설정 하 고 새 SQL Server PDW 어플라이언스를 사용 하 여 시작 하려면 SQL Server PDW 어플라이언스에 단계적으로 안내 합니다.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. 하드웨어 설치  
새 어플라이언스 책장 데이터 센터에 도킹 스테이션에 제공 됩니다.  
  
> [!IMPORTANT]  
> 경우에 따라 프로그램 IHV 됩니다, 그리고 랙, 풀고 기기를 사용자에 대 한 데이터 센터에 연결 합니다. 따라서 이러한 지침은 필요 하지 않습니다. 고으로 건너뛸 수 있습니다는 [3입니다. 어플라이언스 구성](#ConfigureAppliance) 아래 섹션.  
  
프로그램 IHV 하드웨어 설치를 수행 하지 않을 경우 하드웨어를 설치 하려면 다음 단계를 사용 합니다.  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|설명서를 확인 합니다.|모든 필요한 문서 및 정보 (IHV) 독립 하드웨어 공급 업체 로부터 받은 있는지 확인 합니다. 참조 [프로그램 IHV &#40;에서 가져오지 정보 분석 플랫폼 시스템 &#41; ](information-to-obtain-from-your-ihv.md).|  
|하드웨어 설치|어플라이언스를 수용할 수 있는 데이터 센터를 확인 합니다. 데이터 센터에 어플라이언스 구성 요소를 이동 합니다. 네트워크 스위치, Pdu, 랙 및 케이블 연결 합니다. 참조 [하드웨어 설치 &#40; 분석 플랫폼 시스템 &#41; ](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. 어플라이언스에서 전원  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|어플라이언스에서 전원|확인 오류가 발생 하는 데 필요한 대기 하 여 필요한 순서 대로 각 어플라이언스 구성 요소 노드를 켭니다.|  
  
## <a name="ConfigureAppliance"></a>3. 어플라이언스를 구성 합니다.  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|||  
|SQL Server PDW를 사용 하 여 어플라이언스에 구성**Configuration Manager**|어플라이언스 기기 암호, 표준 시간대, 네트워크 및 방화벽 설정, 보안 인증서, 성능 및 기타 설정을 설정 하려면 구성 관리자를 사용 합니다. 참조 [기기 구성 &#40; 분석 플랫폼 시스템 &#41; ](appliance-configuration.md).|  
  
> [!WARNING]  
> SQL Server PDW를 사용 하 여 구성 변경 내용만 해야**Configuration Manager**합니다. 변경 내용을 통해 노출 되지 않는 **Configuration Manager** 지원 되지 않습니다. 예를 들어 SQL Server PDW 어플라이언스에 미국 영어 언어 설정을 지원합니다.  
  
## <a name="SoftwareServicing"></a>4. 소프트웨어 서비스 설정  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|SQL Server PDW 업데이트 적용|(선택 사항) 최신 버전으로 SQL Server PDW 소프트웨어 업데이트에 하나 이상의 SQL Server PDW 업데이트를 적용 해야 합니다. 참조 [분석 플랫폼 시스템 핫픽스 &#40; 적용 분석 플랫폼 시스템 &#41; ](apply-analytics-platform-system-hotfixes.md).|  
|Windows Server Update Services를 구성 합니다.|소프트웨어를 지원 하기 위한 Windows Server Update Services에서 업데이트를 받는 어플라이언스를 구성 합니다. 참조 [다운로드 하 여 Microsoft 업데이트 &#40; 적용 분석 플랫폼 시스템 &#41; ](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>다음 단계  
모든 이전 단계를 완료 한 후 어플라이언스를 사용 하기 위해 있습니다. 다음 작업 또는 기타 인력 사용자 위치에서 시작할 수 있습니다.  
  
|||  
|-|-|  
|**태스크**|**설명**|  
|SQL Server PDW 드라이버를 설치 및 연결 구성|SQL Server Data Tools, sqlcmd, 비즈니스 인텔리전스 소프트웨어 또는 다른 도구를 사용 하 여 SQL Server PDW에 연결 하기 위해 로컬 컴퓨터를 구성 합니다. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|로그온 및 서버 역할을 만들고 사용 권한을 할당합니다|계획 하 고 사용자가 적절 한 권한이 있는 SQL Server PDW에 로그온 할 수 있는 로그온 및 서버 역할을 만들어야 합니다. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Azure 데이터 관리 게이트웨이 구성|APS 데이터 보안 OData 피드를 노출 하 여 온-프레미스 APS 데이터에 액세스 하는 게이트웨이 Azure 있습니다. 게이트웨이 제어 노드에 이미 설치 됩니다. Microsoft 구성 사용 하 여 지원을 요청 합니다.|  
|모니터 쿼리 및 어플라이언스 사용자|관리 콘솔 및 기타 리소스를 사용 하 여 쿼리 및 어플라이언스 사용자가을 모니터링 합니다. 참조 [관리 콘솔 &#40;를 사용 하 여 어플라이언스에 모니터링 분석 플랫폼 시스템 &#41; ](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|SQL Server PDW에 대 한 데이터 로드|데이터 어플라이언스를 로드 합니다. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|재해 복구 계획 만들기|하드웨어 오류 로부터 데이터를 보호 하는 방식과 데이터를 덮어씁니다를 계획 합니다. 정기 백업 미 실시를 사용 하는 계획을 만들고 데이터 손상이 나 손실을 대비 계획을 복원 합니다. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|어플라이언스를 모니터링 합니다.|시스템 뷰, 로그 및 관리 콘솔을 사용 하 여 기기 상태, 상태 및 성능을 모니터링 합니다. 수정 하거나 모든 문제를 보고 합니다. 참조 [모니터 어플라이언스 상태 &#40; 분석 플랫폼 시스템 &#41; ](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
