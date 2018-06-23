---
title: 솔루션 탐색기 원본 제어 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7165143ad238bbbeda14ac91f214f1410082beb2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090238"
---
# <a name="solution-explorer-source-control"></a>솔루션 탐색기 원본 제어
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 솔루션 탐색기는 별도 소스 제어 시스템에 통합할 수 있습니다. 솔루션 또는 프로젝트가 원본 제어 시스템에 통합된 경우 프로젝트에서 스크립트 및 쿼리에 대한 파일 액세스와 버전을 제어할 수 있습니다.  
  
## <a name="solution-and-project-source-control"></a>솔루션 및 프로젝트 원본 제어  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 소스 제어란 서버 소프트웨어의 중심부에서 파일 버전을 저장 및 추적하고 파일에 대한 액세스를 제어하는 시스템을 말합니다. 일반 원본 제어 시스템에는 원본 제어 공급자 및 둘 이상의 원본 제어 클라이언트가 포함됩니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 원본 제어 서비스와 통합할 수 있습니다. 이는 원본 제어 공급자를 위한 클라이언트로서 이 도구를 사용할 수 있다는 것을 의미합니다. 현재 환경에서 이동하지 않은 상태로 개별 및 팀 프로젝트를 쉽게 관리할 수 있습니다. 원본 제어 공급자는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]와 함께 제공되지 않습니다.  
  
#### <a name="to-select-a-source-control-provider"></a>원본 제어 공급자를 선택하려면  
  
1.  원본 제어 공급자의 클라이언트 부분을 설치합니다.  
  
2.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]의 **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
3.  에 **옵션** 대화 상자에서 **소스 제어**, 클릭 하 고는 **플러그 인 선택** 페이지.  
  
4.  에 **현재 소스 제어 플러그 인** 상자에서 소스 제어 플러그 인을 선택 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[원본 제어 기본 사항](../../2014/database-engine/source-control-basics.md)|기본 원본 제어 용어를 정의하고 원본 제어 서비스를 사용할 경우 프로젝트에 어떤 이점이 있는지에 대해 설명합니다.|  
|[원본 제어에 솔루션 및 프로젝트 추가](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 환경을 사용하여 솔루션과 프로젝트를 원본 제어에 추가하는 방법에 대해 설명합니다.|  
|[원본 제어에서 솔루션 및 프로젝트 열기](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 환경을 사용하여 원본 제어 솔루션과 프로젝트를 여는 방법에 대해 설명합니다.|  
|[체크 아웃 관리](../../2014/database-engine/manage-checkouts.md)|솔루션과 파일을 원본 제어에서 체크 아웃하는 방법에 대해 설명합니다.|  
|[체크 인 관리](../../2014/database-engine/manage-checkins.md)|솔루션과 파일을 원본 제어로 체크 인하는 방법에 대해 설명합니다.|  
|[버전 정보 설정 및 검색](../../2014/database-engine/set-and-retrieve-version-information.md)|프로젝트 또는 항목의 기록을 검색하거나 항목의 로컬 복사본을 검색하거나 두 항목 버전을 비교하는 방법에 대해 설명합니다.|  
|||  
  
## <a name="see-also"></a>관련 항목  
 [솔루션 탐색기](../ssms/solution/solution-explorer.md)   
 [솔루션 &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [프로젝트 &#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [솔루션 및 프로젝트 관리 파일](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  