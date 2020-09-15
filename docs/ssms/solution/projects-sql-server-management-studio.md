---
description: 프로젝트(SQL Server Management Studio)
title: 프로젝트(SQL Server Management Studio)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c13af859-ca66-4e43-b76a-0650ac6566c0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 321257f45a593afdaf8c69228b2018347074d7ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417879"
---
# <a name="projects-sql-server-management-studio"></a>프로젝트(SQL Server Management Studio)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 프로젝트는 데이터베이스 관리 및 개발을 위해 함께 저장할 수 있는 논리적으로 연관된 스크립트 및 파일 모음입니다.  
  
## <a name="script-project-overview"></a>스크립트 프로젝트 개요  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트 프로젝트는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 솔루션 탐색기 구성 요소에 표시됩니다. 스크립트 프로젝트는 없거나 1개 이상의 프로젝트 파일을 포함할 수 있습니다. 프로젝트를 솔루션에 추가하거나 솔루션 내에서 둘 이상의 프로젝트를 결합할 수 있습니다.  
  
프로젝트는 다음과 같습니다.  
  
-   **연결**. 프로젝트 내에서 유지되는 연결은 로그인 정보, 서버 이름, 기본 데이터베이스, 기본 설정 프로토콜, 인증 유형, 연결 속성 등을 포함합니다. 연결 정보를 선택적으로 스크립트와 함께 저장할 수 있습니다(아래 참조).  
  
-   **SQLScripts**. 사용자를 위한 자주 사용되는 SQL 스크립트입니다. 프로젝트 내의 .sql 파일을 두 번 클릭하면 SQL 편집기에서 선택한 스크립트가 열립니다.  
  
-   **MDX, DMX 및 XMLAScripts**. 사용자를 위한 자주 사용되는 MDX 스크립트입니다. 프로젝트 내의 .mdx 파일을 두 번 클릭하면 편집기에서 선택한 스크립트가 열립니다.  
  
-   **기타**. 다른 기본 노드 유형에 들어맞지 않는 파일(예: 프로젝트 목표를 포함하는 텍스트 파일)에 이 폴더를 사용할 수 있습니다.  
  
또한 프로젝트를 원본 코드 제어 시스템에 통합할 수 있습니다.  
  
## <a name="connecting-to-an-instance-of-sql-server-from-a-script-project"></a>스크립트 프로젝트에서 SQL Server의 인스턴스에 연결  
스크립트 프로젝트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 연결을 포함할 수 있습니다. 해당 연결을 클릭하여 프로젝트에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다. 이렇게 하면 선택한 연결에 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결된 SQL 스크립트 창이 열립니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 연결로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 MDX 스크립트를 열 경우 편집기가 열리고 스크립트가 로드된 후에 **SQL Server에 연결** 대화 상자에서 암호를 입력하라는 메시지가 나타납니다.  
  
해당 창이 닫히면 연결이 끊어집니다.  
  
연결에 대한 정보를 수정하려면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 속성 창을 사용합니다.  
  
## <a name="project-tasks"></a>프로젝트 태스크  
  
|태스크 설명|항목|  
|--------------------|---------|  
|솔루션에서 새 프로젝트를 만드는 방법에 대해 설명합니다.|[프로젝트 만들기](../../ssms/solution/create-a-project.md)|  
|솔루션에 기존 프로젝트를 추가하는 방법에 대해 설명합니다.|[솔루션에 기존 프로젝트 추가](../../ssms/solution/add-an-existing-project-to-a-solution.md)|  
|프로젝트 파일을 저장할 기본 위치를 변경하는 방법에 대해 설명합니다.|[프로젝트 기본 위치 변경](../../ssms/solution/change-the-default-location-for-projects.md)|  
|프로젝트에 대한 현재 속성을 보는 방법에 대해 설명합니다.|[프로젝트 속성 보기](../../ssms/solution/view-project-properties.md)|  
|프로젝트에 연결, 스크립트 파일 등과 같은 새 항목을 추가하는 방법에 대해 설명합니다.|[프로젝트에 새 항목 추가](../../ssms/solution/add-new-items-to-a-project.md)|  
|쿼리에 대한 연결 정보를 설정하는 방법에 대해 설명합니다.|[쿼리를 프로젝트의 연결 정보로 연결](../../ssms/solution/associate-a-query-with-a-connection-in-a-project.md)|  
|쿼리에 대한 연결 정보를 변경하는 방법에 대해 설명합니다.|[쿼리와 연관된 연결 변경](../../ssms/solution/change-the-connection-associated-with-a-query.md)|  
|연결 속성을 변경하는 방법에 대해 설명합니다.|[프로젝트의 연결 속성 보기 및 변경](../../ssms/solution/view-or-change-the-properties-of-a-connection-in-a-project.md)|  
  
## <a name="see-also"></a>참고 항목  
[솔루션 탐색기](../../ssms/solution/solution-explorer.md)  
[솔루션&#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[솔루션 탐색기 원본 제어](https://docs.microsoft.com/sql/ssms/solution/solution-explorer)  
  
