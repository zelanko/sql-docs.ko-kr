---
title: "SQL Server Management Studio에서 서버 관리 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d73b15b799fe8c52124331cfc346d3759fc860a6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/18/2017

---
# <a name="administer-servers-with-sql-server-management-studio"></a>SQL Server Management Studio에서 서버 관리
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 및 Azure SQL Database 관리자의 서버 관리 요구 사항을 충족하도록 설계된 풍부한 통합 관리 클라이언트입니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]에서는 개체 탐색기를 사용하여 관리 태스크를 수행합니다. 개체 탐색기에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 계열의 서버에 연결하여 서버에 포함된 내용을 도식적으로 찾아볼 수 있습니다. 서버는 [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion_md.md)] 또는 Azure SQL Database의 인스턴스일 수 있습니다.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 의 도구 구성 요소에는 등록된 서버, 개체 탐색기, 솔루션 탐색기, 템플릿 탐색기, 개체 탐색기 정보 페이지 및 문서 창이 포함되어 있습니다. 도구를 표시하려면 **보기** 메뉴에서 도구 이름을 클릭합니다. 쿼리 편집기 도구를 표시하려면 도구 모음에서 **새 쿼리** 단추를 클릭합니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 와 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 간의 네트워크 트래픽은 기본적으로 암호화되지 않습니다. 암호화된 연결이 설정되지 않은 경우 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 에서 중요한 데이터(암호 포함)를 사용하지 마십시오. 자세한 내용은 [방법: 데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006)을 참조하세요.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 를 사용하여 다음을 수행할 수 있습니다.  
  
-   서버 등록  
  
-   [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssAS](../includes/ssas_md.md)], [!INCLUDE[ssRS](../includes/ssrs_md.md)],  [!INCLUDE[ssIS](../includes/ssis_md.md)] 또는 Azure SQL Database의 인스턴스에 연결  
  
-   서버 속성 구성  
  
-   큐브, 차원, 어셈블리 등의 [!INCLUDE[ssAS](../includes/ssas_md.md)] 개체 및 데이터베이스 관리  
  
-   데이터베이스, 테이블, 큐브, 데이터베이스 사용자, 로그인 등의 개체 만들기  
  
-   파일 및 파일 그룹 관리  
  
-   데이터베이스 연결 또는 분리  
  
-   스크립팅 도구 실행  
  
-   보안 관리  
  
-   시스템 로그 보기  
  
-   현재 작업 모니터링  
  
-   복제 구성  
  
-   전체 텍스트 인덱스 관리  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 에이전트를 시작 및 중지하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] 구성 관리자를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 사용](../ssms/use-sql-server-management-studio.md)  
[방법: 서버 속성 보기(SQL Server Management Studio)](http://msdn.microsoft.com/en-us/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  

