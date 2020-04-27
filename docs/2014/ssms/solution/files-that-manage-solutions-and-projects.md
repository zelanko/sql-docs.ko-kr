---
title: 솔루션 및 프로젝트 관리 파일 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e8481c1cce3e43287c04678ddae10ac1b0703af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63044388"
---
# <a name="files-that-manage-solutions-and-projects"></a>솔루션 및 프로젝트 관리 파일
  이 문서에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 고유한 파일 형식에 대해 설명합니다. 기본적으로 모든 솔루션과 해당 프로젝트는 \My Documents\SQL Server Management Studio Projects에서 생성됩니다.  
  
## <a name="management-studio-solution-files"></a>Management Studio 솔루션 파일  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio와 다른 파일 형식을 사용합니다. 이는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션을 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 Visual Studio에서 열 수 없다는 것을 의미합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션 파일의 경우 솔루션 탐색기에서 파일을 관리하기 위한 그래픽 인터페이스를 표시할 수 있습니다.  
  
|내선 번호|파일 형식|Description|만든 사람|  
|---------------|---------------|-----------------|----------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 솔루션 개체|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트, 프로젝트 항목 및 솔루션의 디스크 위치에 대한 참조를 환경에 제공합니다.|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Management Studio 프로젝트 파일  
 솔루션의 개체를 관리하는 솔루션 파일을 솔루션이 포함하는 것과 같은 방식으로 프로젝트는 프로젝트 파일을 포함합니다. 프로젝트에 대해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 가 만드는 프로젝트 파일의 형식은 프로젝트는 만드는 데 사용되는 템플릿에 따라 다릅니다. 다음 표에서는 각 프로젝트에 대해 작성되는 파일 유형을 설명합니다.  
  
|내선 번호|프로젝트 템플릿|  
|---------------|----------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트 프로젝트|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 스크립트 프로젝트|  
  
## <a name="location-of-solution-level-files"></a>솔루션 수준 파일의 위치  
 기본적으로 솔루션 수준 파일은 솔루션을 사용하여 만든 첫 번째 프로젝트의 물리적 디렉터리에 생성됩니다. 솔루션을 만들어 솔루션의 디렉터리를 지정하거나 새 프로젝트를 만들 때 디렉터리를 지정할 수 있습니다.  
  
 솔루션 탐색기에 표시되는 논리적 구조와 비슷한 디렉터리 구조를 갖고 있을 경우 프로젝트 및 솔루션 파일을 더 쉽게 찾고 팀의 다른 개발자와 공유할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [인코딩을 사용 하 여 파일 관리](manage-files-with-encoding.md)   
 [기타 파일](miscellaneous-files.md)   
 [솔루션 탐색기](solution-explorer.md)   
 [솔루션 &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [프로젝트 &#40;SQL Server Management Studio&#41;](projects-sql-server-management-studio.md)   
 [솔루션 탐색기 원본 제어](../../database-engine/solution-explorer-source-control.md)  
  
  
