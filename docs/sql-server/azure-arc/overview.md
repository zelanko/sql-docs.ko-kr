---
title: Azure Arc 지원 SQL Server
titleSuffix: ''
description: Azure Arc 지원 SQL Server를 사용하여 SQL Server 인스턴스 관리
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: references_regions
ms.openlocfilehash: 8312ab1f13d5a85c6dfb43cd29d0ba734846a512
ms.sourcegitcommit: c0f92739c81221fbcdb7c40b53a71038105df44f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91210585"
---
# <a name="azure-arc-enabled-sql-server-preview"></a>Azure Arc 지원 SQL Server(미리 보기)

Azure Arc 지원 SQL Server는 서버용 Azure Arc의 일부입니다. 고객 데이터 센터, 에지 또는 다중 클라우드 환경에서 Azure 외부에 호스트된 SQL Server 인스턴스로 Azure 서비스를 확장합니다.

Azure 서비스를 사용하려면 Azure Portal 및 등록 스크립트를 통해 실행 중인 SQL Server 인스턴스를 Azure Arc에 등록해야 합니다. 등록한 인스턴스는 Azure에서 __SQL Server – Azure Arc__ 리소스로 표시됩니다. 이 리소스의 속성은 SQL Server 반증 설정의 하위 집합을 반영합니다.

연결된 머신 에이전트를 통해 Azure Arc에 연결된, Windows 또는 Linux를 실행하는 가상 머신이나 물리적 머신에 SQL Server를 설치할 수 있습니다. 에이전트를 설치하면 머신이 SQL Server 인스턴스 등록의 일부로 자동으로 등록됩니다. 연결된 머신 에이전트는 TCP 포트 443을 통해 안전하게 Azure Arc로 아웃바운드 통신을 수행합니다. 머신이 인터넷 통신을 위해 방화벽 또는 HTTP 프록시 서버를 통해 연결하는 경우 [연결된 머신 에이전트의 네트워크 구성 요구 사항](/azure/azure-arc/servers/agent-overview#prerequisites)을 검토합니다.

Azure Arc 지원 SQL Server 퍼블릭 미리 보기에서는 데이터 수집 및 보고를 위해 MMA(Microsoft Monitoring Agent) 서버 확장을 설치하고 Azure Log Analytics 작업 영역에 연결해야 하는 솔루션 세트를 지원합니다. 해당 솔루션에는 Azure Security Center 및 Azure Sentinel을 사용하는 고급 데이터 보안과 주문형 SQL 평가 기능을 사용하는 SQL 환경 상태 검사가 포함됩니다.

다음 다이어그램은 Azure Arc 지원 SQL Server의 아키텍처를 보여줍니다.

![퍼블릭 미리 보기 아키텍처](media/overview/pubic-preview-architecture.png)

## <a name="prerequisites"></a>사전 요구 사항

### <a name="supported-sql-versions-and-operating-systems"></a>지원되는 SQL 버전 및 운영 체제

Azure Arc 지원 SQL Server는 다음 버전의 Windows 또는 Linux 운영 체제 중 하나에서 실행되는 SQL Server 2012 이상을 지원합니다.

- Windows Server 2012 R2 이상
- Ubuntu 16.04 및 18.04(x64)
- CentOS Linux 7(x64)
- SLES(SUSE Linux Enterprise Server) 15(x64)

### <a name="required-permissions"></a>필요한 사용 권한

SQL Server 인스턴스 및 호스팅을 Azure Arc에 연결하려면 다음 작업을 수행할 수 있는 권한을 가진 계정이 있어야 합니다.
   * Microsoft.AzureData/sqlServerInstances/write
   * Microsoft.AzureData/sqlServerInstances/read
   * Microsoft.HybridCompute/machines/read
   * Microsoft.HybridCompute/machines/write
   * Microsoft.GuestConfiguration/guestConfigurationAssignments/read

최적 보안을 위해 Azure에서 최소 사용 권한이 나열된 사용자 지정 역할을 만드는 것이 좋습니다. Azure에서 해당 사용 권한을 가진 사용자 지정 역할을 만드는 방법에 대한 자세한 내용은 [사용자 지정 역할 개요](https://docs.microsoft.com/azure/active-directory/users-groups-roles/roles-custom-overview)를 참조하세요. 역할 할당을 추가하려면 [Azure Portal을 사용하여 역할 할당 추가 또는 제거](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) 또는 [Azure RBAC 및 Azure CLI를 사용하여 역할 할당 추가 또는 제거](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-cli)를 참조하세요.

### <a name="azure-subscription-and-service-limits"></a>Azure 구독 및 서비스 한도

Azure Arc를 사용하여 SQL Server 인스턴스와 머신을 구성하기 전에 Azure Resource Manager [구독 한도](/azure/azure-resource-manager/management/azure-subscription-service-limits#subscription-limits) 및 [리소스 그룹 한도](/azure/azure-resource-manager/management/azure-subscription-service-limits#resource-group-limits)를 검토하여 연결할 머신 수를 계획합니다.

### <a name="networking-configuration-and-resource-providers"></a>네트워킹 구성 및 리소스 공급자

연결된 머신 에이전트에 필요한 [네트워킹 구성, 전송 계층 보안, 리소스 공급자](/azure/azure-arc/servers/agent-overview#prerequisites)를 검토합니다.

### <a name="supported-azure-regions"></a>지원되는 Azure 지역

퍼블릭 미리 보기는 다음 지역에서 사용할 수 있습니다.
- 미국 동부
- 미국 동부 2
- 미국 서부 2
- 오스트레일리아 동부
- 동남 아시아
- 북유럽
- 서유럽
- 영국 남부

## <a name="next-steps"></a>다음 단계

- [Azure Arc에 SQL Server 연결](connect.md)
- [SQL Server 인스턴스에 대해 주문형 SQL 평가를 사용한 주기적 환경 상태 검사 구성](assess.md)
- [SQL Server 인스턴스에 대해 고급 데이터 보안 구성](configure-advanced-data-security.md)
