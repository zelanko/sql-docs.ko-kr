---
title: SQL Server 2014에서 지원 되지 않는 관리 도구 기능 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c966c3e4388588810438d7e91a9ae0356ef60c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62780352"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>SQL Server 2014에서 지원되지 않는 관리 도구 기능
  이 항목에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 더 이상 사용할 수 없는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]관리 도구 기능에 대해 설명합니다.  
  
## <a name="features-removed-in-sscurrent"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 제거된 기능  
 없음  
  
## <a name="features-removed-in-sssql11"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 제거된 기능  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 SQL Server Compact Edition 코드 편집기는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 제거되었습니다. SQL Server Compact Edition에 대한 지원도 개체 탐색기, 솔루션 탐색기 및 템플릿 탐색기에서 제거되었습니다. Microsoft Visual Studio 2010 서비스 팩 1 또는 Webmatrix의 Transact-SQL 편집기를 대신 사용하십시오.  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>SQL Server 에이전트용 ActiveX 하위 시스템  
 SQL Server 에이전트용 ActiveX 하위 시스템은 이 릴리스에서 제거되었습니다. 대체 기능은 없습니다.  
  
### <a name="sp_addtask-sp_deletetask-sp_updatetask"></a>sp_addtask, sp_deletetask, sp_updatetask  
 Sp_addtask, sp_deletetask 및 sp_updatetask는 이 릴리스에서 제거되었습니다. 새 애플리케이션이나 업데이트된 애플리케이션에서는 이 기능을 사용하지 마십시오.  
  
### <a name="net-send-and-pager-notification"></a>Net Send 및 호출기 알림  
 Net Send 및 호출기 알림은 이 릴리스에서 제거되었습니다. 새 애플리케이션이나 업데이트된 애플리케이션에서는 이 기능을 사용하지 마십시오.  
  
### <a name="data-tier-applications"></a>데이터 계층 애플리케이션  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 에 있는 일부 DAC(데이터 계층 애플리케이션) 기능은 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 제거되었습니다. 그러나 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]와 함께 출시된 데이터 계층 애플리케이션 프레임워크(DACfx version 3.0)는 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 및 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]를 통해 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]와 호환됩니다. DAC 버전 3.0은 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 의 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 를 포함하여 이전 버전의 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]에서 지원되지 않습니다. Visual Studio 2010 데이터베이스 프로젝트는 DACfx 버전 3.0 이상을 사용하여 생성된 DAC 3.0 DACPAC 패키지 또는 DAC 내보내기(BACPAC) 패키지를 지원하지 않습니다.  
  
 사용 가능한 최신 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 데이터베이스 프로젝트를 사용하는 것이 좋습니다.  
  
 DACfx 3.0 API 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구는 이전 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 도구 및 DACfx 버전을 사용하여 만든 DACPAC 및 BACPAC 파일 읽기를 지원하지 않습니다. 즉, 이 버전에서 DACPAC 파일로 데이터베이스 추출 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Data Tools를 통한 지원되는 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 데이터베이스 배포가 지원되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [이전 버전과의 호환성](../../2014/getting-started/backward-compatibility.md)  
  
  
