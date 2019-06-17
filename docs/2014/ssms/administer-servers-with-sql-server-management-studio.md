---
title: SQL Server Management Studio에서 서버 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9d57657d47f28dc0502b83375f563fa9df737831
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63206816"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>SQL Server Management Studio에서 서버 관리
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 충족 하도록 설계 된 풍부한 통합 관리 클라이언트는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 관리자의 서버 관리 요구 사항입니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서는 개체 탐색기를 사용하여 관리 태스크를 수행합니다. 개체 탐색기에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계열의 서버에 연결하여 서버에 포함된 내용을 도식적으로 찾아볼 수 있습니다. 서버는 [!INCLUDE[ssDE](../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 인스턴스일 수 있습니다.  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 의 도구 구성 요소에는 등록된 서버, 개체 탐색기, 솔루션 탐색기, 템플릿 탐색기, 개체 탐색기 정보 페이지 및 문서 창이 포함되어 있습니다. 도구를 표시하려면 **보기** 메뉴에서 도구 이름을 클릭합니다. 쿼리 편집기 도구를 표시하려면 도구 모음에서 **새 쿼리** 단추를 클릭합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 간의 네트워크 트래픽은 기본적으로 암호화되지 않습니다. 암호화된 연결이 설정되지 않은 경우 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 에서 중요한 데이터(암호 포함)를 사용하지 마십시오. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 를 사용하여 다음을 수행할 수 있습니다.  
  
-   서버 등록  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)], [!INCLUDE[ssAS](../includes/ssas-md.md)], [!INCLUDE[ssRS](../includes/ssrs.md)] 또는 [!INCLUDE[ssIS](../includes/ssis-md.md)]의 인스턴스에 연결합니다.  
  
-   서버 속성 구성  
  
-   큐브, 차원, 어셈블리 등의 [!INCLUDE[ssAS](../includes/ssas-md.md)] 개체 및 데이터베이스 관리  
  
-   데이터베이스, 테이블, 큐브, 데이터베이스 사용자, 로그인 등의 개체 만들기  
  
-   파일 및 파일 그룹 관리  
  
-   데이터베이스 연결 또는 분리  
  
-   스크립팅 도구 실행  
  
-   보안 관리  
  
-   시스템 로그 보기  
  
-   현재 작업 모니터링  
  
-   복제 구성  
  
-   전체 텍스트 인덱스 관리  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트를 시작 및 중지하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자를 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Management Studio 사용](../database-engine/use-sql-server-management-studio.md)   
 [서버 속성 보기 또는 변경&#40;SQL Server&#41;](../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)  
  
  
