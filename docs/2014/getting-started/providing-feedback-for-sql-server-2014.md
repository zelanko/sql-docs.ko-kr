---
title: SQL Server 2014에 대 한 피드백 제공 Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sending feedback to Microsoft
- errors [SQL Server], feedback reporting
- feedback [SQL Server]
- submitting feedback [SQL Server]
- bug reporting [SQL Server]
- reporting usage information to Microsoft
- reporting errors to Microsoft
- SQL Server, feedback reporting
- documentation feedback [SQL Server]
- usage information reporting [SQL Server]
- product feedback [SQL Server]
- automatic error or usage reporting
ms.assetid: 28f3ebf0-ad71-4816-86a6-18a46f023cfe
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10466721f50dd8b090b5d6b1a06b5bffd6e5289d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62772280"
---
# <a name="providing-feedback-for-sql-server-2014"></a>SQL Server 2014에 대한 사용자 의견 제공
  [!INCLUDE[msCoName](../includes/msconame-md.md)]microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 제품 및 설명서를 제품과 개선을 하는 데 도움이 되는 시간을 감사 한다는 메시지가. 제품 기능과 사용자 인터페이스에 대한 제안 사항 및 버그 보고서를 제공하거나 설명서 사용자 의견을 제출하거나 분석을 위해 오류 보고서와 사용량 현황 데이터를 자동으로 [!INCLUDE[msCoName](../includes/msconame-md.md)]에 보낼 수 있습니다. 다음 항목에서는 이러한 세 가지 사용자 의견 옵션 각각에 대해 설명합니다.  
  
## <a name="submitting-feedback-about-the-product"></a>제품에 대한 사용자 의견 보내기  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Connect의 [!INCLUDE[msCoName](../includes/msconame-md.md)] 사용자 의견 페이지를 통해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능에 대한 제안 사항 및 버그 보고서를 보낼 수 있습니다. 이러한 기능에는 도구와 유틸리티, 언어 및 프로그래밍 인터페이스가 포함됩니다.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자 의견 페이지는 다음과 같은 여러 가지 방법으로 찾을 수 있습니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자 의견 [웹 페이지](https://go.microsoft.com/fwlink/?linkid=34178)로 이동합니다.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 도움말 도구 모음에 있는 **사용자 의견 보내기** 단추를 클릭하거나 **커뮤니티/사용자 의견 보내기** 명령을 선택합니다.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 도움말 도구 모음에서 **사용자 의견 보내기** 단추를 클릭합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서에서 모든 항목의 맨 위에 있는 **사용자 의견 보내기** 단추를 클릭합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]나 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서는 다음 중 하나를 수행해야 도움말 도구 모음이 나타납니다.  
  
-   유틸리티에서 도움말에 액세스합니다.  
  
-   **도구/사용자 지정 ...** 명령의 **도구 모음** 탭에서 **도움말** 확인란을 선택 합니다.  
  
## <a name="automatic-error-and-usage-reporting"></a>자동 오류 및 사용 보고  
 자동으로 오류를 보고하고 사용자가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 소프트웨어 및 서비스를 사용하는 방법에 대한 데이터를 보내는 기능을 설정할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)]에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 향상시키는 데 이 정보를 사용하며 모든 데이터는 기밀로 유지됩니다.  
  
### <a name="managing-automatic-usage-reporting"></a>자동 사용 보고 관리  
 자동 사용 보고는 데이터를 수집하여 [!INCLUDE[msCoName](../includes/msconame-md.md)]에 보낼지 여부를 결정하는 데 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 두 개의 파이프라인을 사용하여 사용량 현황 데이터를 보고합니다. 두 개의 파이프라인 모두 유사한 데이터를 보고하지만 서로 다른 프로그램에 대한 데이터를 보고하며 별개로 설정 및 해제할 수 있습니다. 특정 프로그램 중 하나를 사용하여 파이프라인을 설정 또는 해제해도 동일한 파이프라인을 공유하는 다른 프로그램에서의 데이터 수집이 중지 또는 시작됩니다.  
  
-   온라인 설명서 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구의 일부 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 기반 사용자 인터페이스 요소를 제외한 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 사용량 현황 데이터 보고에 하나의 파이프라인이 사용됩니다. 설치가 끝나면 이 파이프라인을 해제(또는 설정)할 수 있습니다. 이를 위해서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기반 프로젝트를 연 다음 **도움말** 메뉴에서 **고객 의견 옵션**을 선택합니다. 이 명령은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기반 프로젝트를 열어야 표시됩니다.  
  
-   다른 파이프라인은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구의 Visual Studio 기반 사용자 인터페이스 요소 및 Visual Studio에 사용됩니다. 설치가 끝나면 이 파이프라인을 해제(또는 설정)할 수 있습니다. 이를 위해서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기반 프로젝트를 연 다음 **도움말** 메뉴에서 **고객 의견 옵션**을 선택합니다. 이 명령은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기반 프로젝트를 열어야 표시됩니다.  
  
## <a name="helping-build-a-better-books-online"></a>보다 나은 온라인 설명서 작성을 위한 기능  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서에 대한 사용 보고를 설정하면 설명서 팀이 더 나은 설명서를 개발하는 데 도움이 됩니다. 수신하는 집계 데이터를 통해 고객의 요구 사항을 파악할 수 있습니다. 즉, 고객이 이동한 항목, 특정 항목을 본 횟수 및 가장 유용하다고 여기는 항목과 가장 유용하지 않다고 여기는 항목을 알 수 있습니다.  
  
 고객의 의견을 통해 고객이 설명서를 어떻게 이용하는지 이해할 수 있습니다. 이에 따라 가장 중요한 항목에 작성 팀을 할당하고 앞으로 사용할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 문서화 시스템을 디자인할 수 있습니다. 온라인 설명서의 이 사용 정보는 고객이 빈번하게 도움말을 찾는 기능을 파악하는 데도 유용합니다. 이를 통해 유용성을 개선해야 하는 영역을 찾을 수 있습니다.  
  
  
