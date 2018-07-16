---
title: 테이블 형식 모델 데이터베이스에 BI 의미 체계 모델 연결 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d1bac7c3bc5e328db1bc54908f1d78ad5829c45
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269939"
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>테이블 형식 model 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기
  SharePoint 팜 외부의 Analysis Services 인스턴스에서 실행되는 테이블 형식 모델 데이터베이스로 리디렉션하는 BI 의미 체계 모델 연결을 설정하려면 이 항목의 정보를 참조합니다.  
  
 BI 의미 체계 모델 연결을 만들고 SharePoint 및 Analysis Services 사용 권한을 구성한 후에는 이 연결을 Excel 또는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서에 데이터 원본으로 사용할 수 있습니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다. 지정된 순서로 각 태스크를 수행하십시오.  
  
 [필수 구성 요소 검토](#bkmk_prereq)  
  
 [공유 서비스 응용 프로그램에 Analysis Services 관리 권한 부여](#bkmk_ssas)  
  
 [테이블 형식 model 데이터베이스에 대한 읽기 권한 부여](#bkmk_BISM)  
  
 [테이블 형식 model 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기](#bkmk_connect)  
  
 [BI 의미 체계 모델 연결에 대한 SharePoint 사용 권한 구성](#bkmk_permissions)  
  
 [다음 단계](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> 필수 구성 요소 검토  
 BI 의미 체계 모델 연결 파일을 만들려면 참가 권한 이상이 있어야 합니다.  
  
 BI 의미 체계 모델 연결 콘텐츠 형식을 지원하는 라이브러리가 있어야 합니다. 자세한 내용은 [라이브러리에 BI 의미 체계 모델 연결 콘텐츠 형식 추가 &#40;SharePoint 용 PowerPivot&#41;](add-bi-semantic-model-connection-content-type-to-library.md)합니다.  
  
 BI 의미 체계 모델 연결을 설정할 서버 및 데이터베이스 이름을 알아야 합니다. Analysis Services를 테이블 형식 모드에 대해 구성해야 합니다. 서버에서 실행 중인 데이터베이스는 테이블 형식 model 데이터베이스여야 합니다. 서버 모드를 확인하는 방법에 대한 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
 특정 시나리오에서 SharePoint 환경의 공유 서비스는 Analysis Services 인스턴스에 대한 관리 권한이 있어야 합니다. 이러한 서비스에는 PowerPivot 서비스 응용 프로그램, Reporting Services 서비스 응용 프로그램 및 PerformancePoint 서비스 응용 프로그램이 포함됩니다. 관리 권한을 부여하기 전에 이러한 서비스 응용 프로그램의 ID를 알고 있어야 합니다. 중앙 관리를 사용하여 ID를 확인할 수 있습니다.  
  
 중앙 관리에서 보안 정보를 보려면 SharePoint 서비스 관리자여야 합니다.  
  
 Management Studio에 대한 관리 권한을 부여하려면 Analysis Services 시스템 관리자여야 합니다.  
  
 SharePoint용 PowerPivot은 클래식 인증 모드를 사용하는 웹 응용 프로그램을 통해 액세스해야 합니다. 외부 데이터 원본에 대한 BI 의미 체계 모델 연결은 클래식 모드 로그인에 종속됩니다. 자세한 내용은 [PowerPivot Authentication and Authorization](power-pivot-authentication-and-authorization.md)합니다.  
  
 연결 시퀀스에 참가하는 모든 컴퓨터 및 사용자는 동일한 도메인이나 트러스트된 도메인(양방향 신뢰)에 있어야 합니다.  
  
##  <a name="bkmk_ssas"></a> 공유 서비스 응용 프로그램에 Analysis Services 관리 권한 부여  
 공유 서비스에서는 데이터를 요청하는 사용자를 대신하여 SharePoint에서 Analysis Services 서버의 테이블 형식 model 데이터베이스로 연결하기도 합니다. 요청하는 서비스는 PowerPivot 서비스 응용 프로그램, Reporting Services 서비스 응용 프로그램 또는 PerformancePoint 서비스 응용 프로그램일 수 있습니다. 연결이 성공하려면 서비스에 Analysis Services 서버에 대한 관리 권한이 있어야 합니다. Analysis Services에서는 관리자만 다른 사용자를 대신하여 가장 연결을 만들 수 있습니다.  
  
 다음과 같은 상황에서 연결을 사용할 경우 관리 권한이 필요합니다.  
  
-   BI 의미 체계 모델 연결 파일 구성 중 연결 정보를 확인할 때  
  
-   BI 의미 체계 모델 연결을 사용하여 파워 뷰 보고서를 시작할 때  
  
-   BI 의미 체계 모델 연결을 사용하여 PerformancePoint 웹 파트를 채울 때  
  
 이러한 동작을 예상대로 수행하려면 각 서비스 ID에 Analysis Services 인스턴스에 대한 관리 권한을 부여합니다. 필요한 권한을 부여하려면 다음 지침을 따르십시오.  
  
 **서버 관리자 역할에 서비스 ID 추가**  
  
1.  SQL Server Management Studio에서 Analysis Services 인스턴스에 연결합니다.  
  
2.  서버 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **보안**을 클릭한 다음 **추가**를 클릭합니다. 서비스 응용 프로그램을 실행하는 데 사용되는 Windows 사용자 계정을 입력합니다.  
  
     중앙 관리를 사용하여 ID를 확인할 수 있습니다. 보안 섹션에서 **서비스 계정 구성** 을 열고 각 응용 프로그램에서 사용되는 서비스 응용 프로그램 풀과 연결된 Windows 계정을 확인한 후 이 항목에 제공된 지침에 따라 계정 관리 권한을 부여합니다.  
  
##  <a name="bkmk_BISM"></a> 테이블 형식 model 데이터베이스에 대한 읽기 권한 부여  
 데이터베이스가 팜 외부에 있는 서버에서 실행 중이므로 연결을 설정하려면 백 엔드 Analysis Services 서버에 대한 데이터베이스 사용자 권한을 부여해야 합니다. Analysis Services에서는 역할 기반 권한 모델을 사용합니다. model 데이터베이스에 연결하는 사용자는 해당 멤버에게 읽기 권한을 부여하는 역할을 통해 읽기 권한 이상을 사용하여 연결해야 합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 만들 때 역할 또는 역할 멤버 자격이 정의됩니다. SQL Server Management Studio로 역할을 만들 수 있지만, 이미 정의된 역할에 멤버를 추가할 수는 없습니다. 역할을 만드는 방법에 대한 자세한 내용은 [역할 만들기 및 관리&#40;SSAS 테이블 형식&#41;](../tabular-models/roles-ssas-tabular.md)를 참조하세요.  
  
#### <a name="assign-role-membership"></a>역할 멤버 자격 할당  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 데이터베이스를 확장한 다음 **역할**을 확장합니다. 이미 정의된 역할이 표시됩니다. 역할이 없는 경우 모델 작성자에게 연락하여 추가 또는 역할을 요청하십시오. 모델을 다시 배포해야 역할이 Management Studio에 표시됩니다.  
  
2.  역할을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  멤버 자격 페이지에서 액세스 권한이 필요한 Windows 그룹 및 사용자 계정을 추가합니다.  
  
##  <a name="bkmk_connect"></a> 테이블 형식 model 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기  
 Analysis Services에서 사용 권한을 설정한 후 SharePoint로 돌아가서 BI 의미 체계 모델 연결을 만들 수 있습니다.  
  
1.  BI 의미 체계 모델 연결이 포함될 라이브러리의 SharePoint 리본에서 **문서** 를 클릭합니다.  
  
2.  새 문서에서 아래쪽 화살표를 클릭하고 **BI 의미 체계 모델 연결 파일** 을 선택하여 새 BI 의미 체계 모델 연결 페이지를 엽니다.  
  
3.  **서버** 및 **데이터베이스** 속성을 설정합니다. 데이터베이스 이름을 모를 경우 SQL Server Management Studio를 사용하여 서버에 배포된 데이터베이스의 목록을 확인합니다.  
  
     **서버 이름** 은 서버의 네트워크 이름, IP 주소 또는 정규화된 도메인 이름(예: myserver.mydomain.corp.adventure-works.com)입니다. 서버가 명명된 인스턴스로 설치된 경우 computername\instancename 형식으로 서버 이름을 입력합니다.  
  
     **데이터베이스** 는 서버에서 현재 사용할 수 있는 테이블 형식 데이터베이스여야 합니다. 다른 BI 의미 체계 모델 연결 파일, Office 데이터 연결(.odc) 파일, Analysis Services OLAP 데이터베이스 또는 PowerPivot 통합 문서를 지정하지 마십시오. 데이터베이스 이름을 가져오려면 Management Studio를 사용하여 서버에 연결하고 사용 가능한 데이터베이스 목록을 볼 수 있습니다. 데이터베이스의 속성 페이지를 사용하여 이름이 올바른지 확인합니다.  
  
4.  **확인** 을 클릭하여 페이지를 저장합니다. 이 시점에서 PowerPivot 서비스 응용 프로그램은 연결을 확인합니다.  
  
     연결 정보가 정확하고 PowerPivot 서비스 응용 프로그램에 관리 권한을 부여하여 Analysis Services에 현재 사용자로 연결할 수 있으면 확인이 성공합니다.  
  
     연결 정보가 잘못되었거나 서비스 응용 프로그램에 권한이 부족하면 확인이 실패합니다. 유효성 검사 메시지는 파일 저장 여부를 묻는 페이지에 표시됩니다. 연결이 유효함을 알고 있을 경우 연결 정보가 잘못되어서가 아니라 권한이 없어서 오류가 발생한 것이므로 파일을 저장해야 합니다.  
  
     Excel 또는 파워 뷰에서 연결을 사용하여 테이블 형식 model 데이터베이스에 연결함으로써 연결을 확인할 수 있습니다. 데이터 원본 연결에 성공하면 확인 경고가 나타나더라도 연결이 유효한 것입니다.  
  
##  <a name="bkmk_permissions"></a> BI 의미 체계 모델 연결에 대한 SharePoint 사용 권한 구성  
 BI 의미 체계 모델 연결을 Excel 통합 문서 또는 Reporting Services 보고서의 데이터 원본으로 사용하려면 SharePoint 라이브러리의 BI 의미 체계 모델 연결 항목에 대해 **읽기** 권한이 있어야 합니다. 읽기 권한 수준에는 BI 의미 체계 모델 연결 정보를 Excel 데스크톱 응용 프로그램에 다운로드할 수 있는 **항목 열기** 권한이 포함되어 있습니다.  
  
 여러 가지 방법으로 SharePoint에서 사용 권한을 부여할 수 있습니다. 다음은 **읽기** 수준의 권한이 있는 **BISM Users** 라는 새 그룹을 만드는 방법을 설명하는 지침입니다.  
  
 사용 권한을 변경하려면 사이트 소유자여야 합니다.  
  
1.  사이트 작업에서 **사이트 사용 권한**을 클릭합니다.  
  
2.  **그룹 만들기** 를 클릭하고 새 그룹의 이름을 **BISM Users**로 지정합니다.  
  
3.  **읽기** 권한 수준을 선택한 다음 **만들기**를 클릭합니다.  
  
4.  사용자 및 그룹에서 **BISM Users** 를 선택합니다.  
  
5.  새로 만들기를 가리키고 **사용자 추가**를 클릭한 다음 사용자 또는 그룹 계정을 추가합니다.  
  
     이 사용자 및 그룹은 이제 사이트 수준에서 사용 권한을 상속하는 모든 라이브러리와 목록을 포함하여 사이트 전체에서 읽기 권한이 있습니다. 이 사용 권한이 너무 높은 경우 특정 라이브러리, 목록 또는 항목에서 이 그룹을 선택적으로 제거할 수 있습니다.  
  
 항목 수준에서 사용 권한을 선택적으로 제거하려면 다음을 수행합니다.  
  
1.  라이브러리에서 문서를 선택합니다. 오른쪽 아래 화살표를 클릭한 다음 **사용 권한 관리**를 클릭합니다.  
  
2.  기본적으로 항목은 사용 권한을 상속합니다. 이 라이브러리에서 개별 문서의 사용 권한을 변경하려면 **권한 상속 중지**를 클릭합니다.  
  
3.  **BISM Users**옆에 있는 확인란을 선택합니다.  
  
4.  **사용자의 사용 권한 제거**를 클릭합니다.  
  
##  <a name="bkmk_next"></a> 다음 단계  
 BI 의미 체계 모델 연결을 만들고 확인한 후 데이터 원본으로 지정할 수 있습니다. 자세한 내용은 [Excel 또는 Reporting Services에서 BI 의미 체계 모델 연결 사용](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [PowerPivot BI 의미 체계 모델 연결 &#40;.bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [PowerPivot 통합 문서에 대한 BI 의미 체계 모델 연결 만들기](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
