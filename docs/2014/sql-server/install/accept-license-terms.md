---
title: 사용 조건에 동의 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 55d500b13cc3ab3c859474bb3050e29a7487f4a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186890"
---
# <a name="accept-license-terms"></a>사용 조건 동의
  **설치 마법사의** 사용 조건 동의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]릴리스의 사용 조건에 동의할 수 있습니다.  
  
 사용권 계약은 인쇄하거나 클립보드로 복사할 수 있습니다. 계속하려면 사용 조건에 동의하고 **다음**을 클릭합니다. 설치를 종료하려면 **취소**를 클릭합니다.  
  
## <a name="customer-experience-improvement-program-ceip"></a>CEIP(Customer Experience Improvement Program)  
 CEIP 보고를 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 보고서를 주기적으로 보내도록 구성됩니다. 보고서에는 하드웨어 구성 정보와 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 구성 요소를 사용하는 방식이 포함됩니다. 기능 사용 데이터는 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 개선하는 데 사용됩니다. 이 기능을 통해 모니터링되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 다음과 같습니다.  
  
-   는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   복제  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램  
  
 기능 사용에 대한 정보는 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보내지며 제한된 액세스로 저장됩니다.  
  
 설치가 완료된 후에 CEIP 보고를 해제하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**구성 도구** 메뉴의 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 및 사용 보고** 도구를 사용합니다.  
  
 설치, 업그레이드 및 복구와 같은 설치 동작에 대한 정보는 설치 프로그램이 실행되는 동안에만 수집되어 업로드됩니다.  
  
 다른 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소에 대한 정보는 설정된 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대해 하루에 한 번씩 수집됩니다. 수집 시간은 서버 로드를 최소화하기 위해 기본적으로 자정으로 설정됩니다. 수집 시간을 변경하려는 경우 수집 시간을 제어하는 레지스트리 키를 수동으로 편집할 수 있습니다. 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에는 다음과 같은 자체 레지스트리 키가 있습니다.  
  
 HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\mssql12.<instancename>\mssql\.\< INSTANCEID > \CPE\TimeofReporting  
  
 이 레지스트리 키 값에는 수집 실행 시간이 00:00(자정)부터 경과된 분 수로 포함되어 있습니다. 예를 들어 값 60은 오전1시에 수집이 실행되었음을 나타내고 값 1200은 오후 8시에 수집이 실행되었음을 나타냅니다.  
  
## <a name="error-reporting"></a>오류 보고  
 **설치 마법사의** 오류 및 사용 보고서 설정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기능 오류 및 사용 보고 기능을 설정할 수 있습니다.  
  
### <a name="options"></a>변수  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 해당 구성 요소의 기능 사용 데이터 컬렉션 및 오류 보고 기능은 기본적으로 해제되어 있습니다.  
  
 오류 보고  
 오류 보고 기능을 설정하면 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소 중 하나에서 오류가 발생할 경우 자동으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에 보고서를 보내도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 구성됩니다.  
  
-   는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   복제  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 오류 보고서를 사용 하 여 개선 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 하며 모든 정보는 기밀로 처리 합니다.  
  
 오류 정보는 보안 연결(HTTPS)을 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)]로 보내며 액세스가 제한된 곳에 보관됩니다. 또는 사용자의 회사 오류 보고 서버 서버로 오류 보고서를 보낼 수 있습니다.  
  
 오류 보고서에는 다음 정보가 포함됩니다.  
  
-   문제 발생 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 상태  
  
-   운영 체제 버전 및 컴퓨터 하드웨어 정보  
  
-   라이선스 확인에 사용되지 않는 디지털 제품 ID  
  
-   컴퓨터 또는 프록시 서버의 네트워크 IP 주소  
  
-   오류가 발생한 프로세스의 메모리 또는 파일 정보  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 고의로 수집 하지 않습니다 파일, 이름, 주소, 전자 메일 주소 또는 기타 형태의 개인 정보입니다. 그러나 오류 보고서에는 오류를 발생시킨 프로세스의 메모리나 파일에 있는 개인 정보가 포함될 수 있습니다. 이런 정보는 사용자의 신분을 확인하는 데 사용될 가능성은 있지만 [!INCLUDE[msCoName](../../includes/msconame-md.md)]에서 의도적으로 사용하지는 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개인 정보 보호 및 데이터 수집 정책에 대한 자세한 내용은 [Microsoft SQL Server 개인 정보 취급 방침](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md)을 참조하세요.  
  
 오류 보고를 설정한 상태에서 오류가 발생하면 특정 오류에 대한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 문서를 가리키는 Windows 이벤트 로그의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 응답을 볼 수 있습니다.  
  
 설치가 완료된 후에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 해당 구성 요소의 모든 인스턴스에 대해 오류 또는 기능 사용 보고를 해제하려면 **오류 및 사용 보고 설정** 대화 상자로 가서 **기능 사용**확인란의 선택을 취소합니다. **오류 보고**가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 여러 구성 요소([!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 공유 구성 요소)에 대해 설정되어 있으면 **기타**로 표시된 공유 구성 요소뿐만 아니라 개별 구성 요소의 각 인스턴스에 대해 오류 보고를 해제할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 사용 조건 정보](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  