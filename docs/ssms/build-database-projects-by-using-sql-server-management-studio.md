---
title: SQL Server Management Studio를 사용하여 데이터베이스 프로젝트 빌드 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], database projects
- database projects [SQL Server]
- projects [SQL Server Management Studio], about projects
- projects [SQL Server Management Studio]
ms.assetid: c2e80045-894d-44cf-b65c-e547ed738947
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3dda4b94a26b0a2e88d6ad9be75abfa6721cd77
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="build-database-projects-by-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 데이터베이스 프로젝트 빌드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
데이터베이스 스크립트 프로젝트는 데이터베이스와 관련되거나 데이터베이스의 일부인 스크립트, 연결 정보 및 템플릿으로 구성된 집합입니다. [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 스크립트 프로젝트의 컨텍스트 내에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 데이터베이스를 관리하고 디자인할 수 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 를 제공합니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 사용자의 데이터베이스 개발, 배포 및 유지 관리를 도와 주는 디자이너, 편집기, 지침 및 마법사가 포함되어 있습니다.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]에 속한 구성 요소를 관리하는 관리 도구 모음입니다. 이 통합 환경에서는 단일 인터페이스로 데이터 백업, 쿼리 편집, 일반 기능 자동화 등의 다양한 태스크를 수행할 수 있습니다.  
  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 다음 도구가 포함되어 있습니다.  
  
-   스크립트를 작성하고 편집할 수 있는 유용한 스크립트 편집기인 코드 편집기 - [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)][!INCLUDE[ssDE](../includes/ssde_md.md)] 스크립트용 [!INCLUDE[tsql](../includes/tsql_md.md)] 쿼리 편집기, DMX 쿼리 편집기, MDX 쿼리 편집기 및 XML/A 쿼리 편집기라는 4가지 버전의 코드 편집기를 제공합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]인스턴스에 속한 개체를 찾고 수정하고 스크립팅하거나 실행하는 개체 탐색기  
  
-   템플릿을 찾고 스크립팅하는 템플릿 탐색기  
  
-   관련 스크립트를 프로젝트의 일부로 구성하고 저장하는 솔루션 탐색기  
  
-   선택한 개체의 현재 속성을 표시하는 속성 창  
  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 다음을 제공하여 효율적인 작업 프로세스를 지원합니다.  
  
-   연결이 끊긴 액세스 - [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)]인스턴스에 연결하지 않고도 스크립트를 작성하고 편집할 수 있습니다.  
  
-   모든 대화 상자에서 스크립팅 - 어떤 대화 상자에서든 스크립트를 작성한 후 읽고 수정하고 저장하거나 다시 사용할 수 있습니다.  
  
-   비모달 대화 상자 - UI 대화 상자에 액세스할 때 대화 상자를 닫지 않고도 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 의 다른 리소스를 찾아볼 수 있습니다.  
  
## <a name="solutions-and-script-projects"></a>솔루션 및 스크립트 프로젝트  
솔루션 탐색기는 데이터베이스 솔루션을 저장하고 다시 열기 위한 유틸리티입니다. 솔루션은 관련 스크립트 프로젝트와 파일로 구성되며 스크립트 프로젝트는 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 스크립트 파일, SQL 템플릿, 연결 정보 및 기타 파일을 저장합니다. 스크립트가 스크립트 프로젝트에 저장되어 있을 경우 다음 작업을 할 수 있습니다.  
  
-   스크립트 버전 제어를 유지 관리합니다.  
  
-   스크립트와 함께 결과 옵션을 저장합니다.  
  
-   단일 스크립트 프로젝트로 관련 스크립트를 조직화합니다.  
  
-   스크립트와 함께 연결 정보를 저장합니다.  
  
솔루션 탐색기는 같은 프로젝트에 관련된 스크립트를 작성하고 다시 사용하기 위한 개발자용 도구입니다. 나중에 유사한 태스크가 필요할 경우 프로젝트에 저장된 스크립트 그룹을 사용할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[vsprvs](../includes/vsprvs_md.md)]를 사용하여 응용 프로그램을 만들어 본 경험이 있다면 솔루션 탐색기가 전혀 낯설지 않을 것입니다.  
  
솔루션은 하나 이상의 스크립트 프로젝트로 구성됩니다. 프로젝트는 하나 이상의 스크립트 또는 연결로 구성되며 스크립트가 아닌 파일도 포함할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 사용](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio에서 쿼리 작성, 분석 및 편집](http://msdn.microsoft.com/en-us/062051e4-4b77-4969-98ae-d2547c24ce3e)  
[솔루션&#40;SQL Server Management Studio&#41;](../ssms/solution/solutions-sql-server-management-studio.md)  
  
