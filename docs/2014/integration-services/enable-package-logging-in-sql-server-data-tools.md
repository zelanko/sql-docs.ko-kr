---
title: 에서 패키지 로깅 사용 SQL Server 데이터 도구 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a93245b97bf7c6c382f533c6d6e317b399f9e54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172503"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>SQL Server Data Tools에서 패키지 로깅 사용
  이 절차에서는 패키지에 로그를 추가하는 방법, 패키지 수준 로깅을 구성하는 방법 및 로깅 구성을 XML 파일에 저장하는 방법을 설명합니다. 로그는 패키지 수준에서만 추가할 수 있지만 패키지에 포함되는 컨테이너에서 로깅을 활성화하기 위해 패키지가 로깅을 수행할 필요는 없습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 배포하는 경우 패키지 실행에 대해 설정한 로깅 수준에 따라 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 사용하여 구성하는 패키지 로깅이 재정의됩니다.  
  
 기본적으로 패키지 내의 컨테이너는 부모 컨테이너와 동일한 로깅 구성을 사용합니다. 개별 컨테이너에 대한 로깅 옵션을 설정하는 방법은 [저장된 구성 파일을 사용하여 로깅 구성](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md)을 참조하세요.  
  
### <a name="to-enable-logging-in-a-package"></a>패키지에 로깅을 활성화하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **SSIS** 메뉴에서 **로깅**을 클릭합니다.  
  
3.  **공급자 유형** 목록에서 로그 공급자를 선택한 다음 **추가**를 클릭합니다.  
  
4.  **구성** 열에서 연결 관리자를 선택하거나 **\<새 연결>** 을 클릭하여 로그 공급자에 대한 적절한 유형의 연결 관리자를 만듭니다. 선택한 공급자에 따라 다음 연결 관리자 중 하나를 사용합니다.  
  
    -   텍스트 파일에는 파일 연결 관리자를 사용합니다. 자세한 내용은 [File Connection Manager](connection-manager/file-connection-manager.md)를 참조하세요.  
  
    -   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]에는 파일 연결 관리자를 사용합니다.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에는 OLE DB 연결 관리자를 사용합니다. 자세한 내용은 [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
    -   Windows 이벤트 로그에는 아무 것도 선택하지 마십시오. [!INCLUDE[ssIS](../includes/ssis-md.md)] 로그를 자동으로 만듭니다.  
  
    -   XML 파일에는 파일 연결 관리자를 사용합니다.  
  
5.  패키지에서 사용할 각 로그에 대해 3단계 및 4단계를 반복합니다.  
  
    > [!NOTE]  
    >  패키지는 각 유형의 로그를 두 개 이상 사용할 수 있습니다.  
  
6.  필요에 따라 패키지 수준 확인란을 선택하고 패키지 수준 로깅에서 사용할 로그를 선택한 다음 **세부 정보** 탭을 클릭합니다.  
  
7.  **자세히** 탭에서 **이벤트** 를 선택하여 모든 로그 항목을 로깅하거나 **이벤트** 선택을 취소하여 개별 이벤트를 선택합니다.  
  
8.  필요에 따라 **고급** 을 클릭하여 로깅할 정보를 지정합니다.  
  
    > [!NOTE]  
    >  기본적으로 모든 정보가 로깅됩니다.  
  
9. **세부 정보** 탭에서 **저장**을 클릭합니다. **다른 이름으로 저장** 대화 상자가 나타납니다. 로깅 구성을 저장할 폴더를 찾고 새 로그 구성의 파일 이름을 입력한 다음 **저장**을 클릭합니다.  
  
10. **확인**을 클릭합니다.  
  
11. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services &#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)   
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)  
  
  
