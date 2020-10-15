---
title: Advanced Data Security 구성
titleSuffix: Azure Arc
description: Azure Arc 사용 SQL Server 인스턴스에 대해 Advanced Data Security 구성
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 2bd589ebacd9ea35e15881eaaeb022d4f2302986
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988029"
---
# <a name="configure-advanced-data-security-for-azure-arc-enabled-sql-server-instance"></a>Azure Arc 사용 SQL Server 인스턴스에 대해 Advanced Data Security 구성

다음 단계를 수행하여 온-프레미스에서 SQL Server 인스턴스에 Advanced Data Security를 사용하도록 설정할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

* SQL Server 인스턴스가 Arc 사용 SQL Server에 온보딩되어 있습니다. 지침에 따라 [SQL Server 인스턴스를 Arc 사용 SQL Server에 온보딩](connect.md)합니다.

* 사용자 계정에 [Security Center 역할(RBAC)](/azure/security-center/security-center-permissions) 중 하나가 할당되었습니다.

## <a name="create-a-log-analytics-workspace"></a>Log Analytics 작업 영역 만들기

1. __Log Analytics 작업 영역__ 리소스 종류를 검색하고 만들기 블레이드를 통해 새 항목을 추가합니다.

   ![새 작업 영역 만들기](media/configure-advanced-data-security/create-new-log-analytics-workspace.png)

   > [!NOTE]
   > Log Analytics 작업 영역 1개를 모든 지역에서 사용할 수 있으므로 이미 있는 경우 기존 작업 영역을 사용할 수 있습니다. 하지만 __머신 - Azure Arc__ 리소스가 생성되는 곳과 동일한 지역에 작업 영역을 만드는 것이 좋습니다.

1. Log Analytics 작업 영역 리소스의 개요 페이지로 이동하여 “Windows, Linux, 기타 원본”을 선택합니다. 나중에 사용하기 위해 작업 영역 ID와 기본 키를 복사합니다.

   ![Log Analytics 작업 영역 블레이드](media/configure-advanced-data-security/log-analytics-workspace-blade.png)

## <a name="install-microsoft-monitoring-agent-mma"></a>MMA(Microsoft Monitoring Agent) 설치

다음 단계는 원격 머신에서 MMA 에이전트를 아직 구성하지 않은 경우에만 필요합니다.

1. SQL Server 인스턴스가 설치된 가상 서버 또는 물리적 서버에 대한 __머신 - Azure Arc__ 리소스를 선택하고 **확장** 기능을 사용하여 __Microsoft Monitoring Agent - Azure Arc__ 확장을 추가합니다. Log Analytics 작업 영역을 구성하라는 메시지가 표시되면 이전 단계에서 저장한 작업 영역 ID와 기본 키를 사용합니다.

   ![MMA 설치](media/configure-advanced-data-security/install-mma-extension.png)

1. 유효성 검사에 성공한 후 **만들기**를 클릭하여 MMA Arc 확장 배포 워크플로를 시작합니다. 배포가 완료되면 상태가 **성공**으로 업데이트됩니다.

1. 자세한 내용은 [Azure Arc를 사용한 확장 관리](/azure/azure-arc/servers/manage-vm-extensions)를 참조하세요.

## <a name="enable-advanced-data-security"></a>Advanced Data Security 사용

다음에는 SQL Server 인스턴스에 Advanced Data Security를 사용하도록 설정해야 합니다.

1. Security Center로 이동하여 사이드바에서 **가격 책정 및 설정** 페이지를 엽니다.

1. 이전 단계에서 MMA 확장에 대해 구성한 작업 영역을 선택합니다.

1. **표준**을 선택합니다. **머신의 SQL Server(미리 보기)** 옵션이 사용하도록 설정되어 있는지 확인합니다.

   ![작업 영역 업그레이드](media/configure-advanced-data-security/upgrade-log-analytics-workspace.png)

 > [!NOTE]
   > 취약성 평가를 생성하는 첫 번째 검사는 Advanced Data Security를 사용하도록 설정한 후 24시간 이내에 수행됩니다. 그런 다음, 매주 일요일에 자동 검사가 수행됩니다.

## <a name="explore"></a>탐색

Azure Security Center에서 보안 변칙 및 위협을 살펴봅니다.

1. SQL Server - Azure Arc 리소스를 열고 왼쪽 메뉴에서 **보안**을 선택하여 해당 인스턴스에 대한 권장 사항 및 경고를 확인합니다.

   ![보안 제목 선택](media/configure-advanced-data-security/security-heading-sql-server-arc.png)

1. 권장 사항 중 하나를 클릭하여 __Security Center__에서 취약성 세부 정보를 확인합니다.

   ![취약성 보고서](media/configure-advanced-data-security/vulnerabilities-report.png)

1. 보안 경고를 클릭하여 전체 세부 정보를 확인하고 [Azure Sentinel](/azure/sentinel/overview)에서 공격을 살펴봅니다. 다음 다이어그램은 무차별 암호 대입(brute force) 경고의 예입니다.

   ![무차별 암호 대입 경고](media/configure-advanced-data-security/brute-force-alert.png)

1. **작업 수행**을 클릭하여 경고를 완화합니다.

   ![경고 완화](media/configure-advanced-data-security/brute-force-alert-mitigation.png)

> [!NOTE]
> 페이지 맨 위에 있는 일반적인 __Security Center__ 링크는 미리 보기 포털 URL을 사용하지 않으므로 __SQL Server - Azure Arc__ 리소스가 표시되지 않습니다. 개별 권장 사항 또는 경고 링크를 따르는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

[Azure Sentinel](/azure/sentinel/overview)을 사용하여 보안 경고 및 공격을 자세히 조사할 수 있습니다. 지침에 따라 [Azure Sentinel을 온보딩](/azure/sentinel/connect-data-sources)합니다.