---
title: SQL Server Management Studio에서 서버 관리
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], administering
ms.assetid: 938bb035-e07a-4082-9f93-229d9feb6b06
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fdf38619102dde1ecf5b8e92f70ec2ea79c77811
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254529"
---
# <a name="administer-servers-with-sql-server-management-studio"></a>SQL Server Management Studio에서 서버 관리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 Azure SQL Database 관리자의 서버 관리 요구 사항을 충족하도록 설계된 풍부한 통합 관리 클라이언트입니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서는 개체 탐색기를 사용하여 관리 태스크를 수행합니다. 개체 탐색기에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계열의 서버에 연결하여 서버에 포함된 내용을 도식적으로 찾아볼 수 있습니다. 서버는 [!INCLUDE[ssDE](../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 또는 Azure SQL Database의 인스턴스일 수 있습니다.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 의 도구 구성 요소에는 등록된 서버, 개체 탐색기, 솔루션 탐색기, 템플릿 탐색기, 개체 탐색기 정보 페이지 및 문서 창이 포함되어 있습니다. 도구를 표시하려면 **보기** 메뉴에서 도구 이름을 클릭합니다. 쿼리 편집기 도구를 표시하려면 도구 모음에서 **새 쿼리** 단추를 클릭합니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 간의 네트워크 트래픽은 기본적으로 암호화되지 않습니다. 암호화된 연결이 설정되지 않은 경우 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 에서 중요한 데이터(암호 포함)를 사용하지 마십시오. 자세한 내용은 [방법: 데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006)을 참조하세요.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 를 사용하여 다음을 수행할 수 있습니다.  
  
-   서버 등록  
  
-   [!INCLUDE[ssDE](../includes/ssde_md.md)], SSAS, [!INCLUDE[ssRS](../includes/ssrs.md)], [!INCLUDE[ssIS](../includes/ssis_md.md)] 또는 Azure SQL Database의 인스턴스에 연결합니다.  
  
-   서버 속성 구성  
  
-   큐브, 차원, 어셈블리 등의 데이터베이스 및 SSAS 개체를 관리합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 사용](../ssms/use-sql-server-management-studio.md)  
[방법: 서버 속성 보기(SQL Server Management Studio)](https://msdn.microsoft.com/55f3ac04-5626-4ad2-96bd-a1f1b079659d)  
  
