---
title: Power Pivot 인증 및 권한 부여 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2ebb63d1ad381982ab4313ee6d980c5a919d6122
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="power-pivot-authentication-and-authorization"></a>Power Pivot 인증 및 권한 부여
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  SharePoint 2010 팜에서 실행되는 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 배포에서는 SharePoint 서버에서 제공되는 인증 하위 시스템과 권한 부여 모델을 사용합니다. 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관련 콘텐츠는 SharePoint 콘텐츠 데이터베이스에 저장되고 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]관련 작업은 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]공유 서비스에 의해 수행되므로 SharePoint 보안 인프라는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 콘텐츠 및 작업까지 포함합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터가 포함된 통합 문서를 요청하는 사용자는 Windows 사용자 ID를 기반으로 하는 SharePoint 사용자 ID를 사용하여 인증됩니다. 통합 문서에 대한 보기 권한에 따라 요청을 허용할지 여부가 결정됩니다.  
  
 셀프 서비스 데이터 분석을 위해 Excel Services와 통합해야 하므로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버를 보호하려면 Excel Services 보안에 대해서도 잘 알고 있어야 합니다. 사용자가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 데이터 연결이 있는 피벗 테이블을 쿼리할 경우 Excel 서비스에서는 데이터 연결 요청을 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에 전달하여 데이터를 로드합니다. 서버 간의 이러한 상호 작용을 위해서는 각 서버에서 보안 설정을 구성하는 방법을 잘 알고 있어야 합니다.  
  
 이 항목의 특정 섹션을 보려면 다음 링크를 클릭하십시오.  
  
 [클래식 모드 로그인 요구 사항을 사용한 Windows 인증](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [사용자 권한 부여를 요구하는 Power Pivot 작업](#UserConnections)  
  
 [Power Pivot 데이터 액세스에 대한 SharePoint 사용 권한](#Permissions)  
  
 [Excel 서비스 보안 고려 사항: Power Pivot 통합 문서](#excel)  
  
##  <a name="bkmk_auth"></a> 클래식 모드 로그인 요구 사항을 사용한 Windows 인증  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 은 SharePoint에 제공되는 인증 옵션 중 일부만 지원합니다. 즉, SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 배포에서는 사용 가능한 인증 옵션 중 Windows 인증만 지원합니다. 또한 로그인을 실행하는 웹 응용 프로그램은 클래식 모드로 구성되어야 합니다.  
  
 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 배포의 Analysis Services 데이터 엔진이 Windows 인증만 지원하므로 Windows 인증은 필수입니다. Excel 서비스는 MSOLAP OLE DB 공급자를 통해 Analysis Services에 대한 연결을 설정할 때 NTLM 또는 Kerberos 프로토콜을 통해 인증되는 Windows 사용자 ID를 사용합니다.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 웹 서비스가 작동하려면 두 번째 요구 사항으로 웹 응용 프로그램의 클래식 모드 인증이 필요합니다. 웹 서비스는 웹 프런트 엔드에서 실행되어 팜의 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에 HTTP 리디렉션을 제공하는 구성 요소입니다. 이 웹 서비스는 서비스 간 통신에 대한 클레임은 인식하지만 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공유 서비스로 라우팅하는 데이터 연결 요청에 대한 클레임은 인식하지 못합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 로드하는 요청은 IIS에서 시작되어 Windows ID를 사용하여 인증된 연결에서만 지원됩니다. 웹 응용 프로그램에서 클래식 모드로 로그인하면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 웹 서비스와 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공유 서비스 간 연결이 설정됩니다.  
  
 더 일반적인 데이터 액세스 시나리오( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터가 데이터를 렌더링하는 동일한 Excel 통합 문서에서 추출되는 경우)에는 클래식 모드 로그인이 필요하지 않지만, SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 을 다른 인증 공급자를 사용하도록 구성된 SharePoint 웹 응용 프로그램과 함께 사용하지 마세요. 그렇게 하면 사용자가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 외부 데이터 원본으로 연결하려고 할 때마다 연결이 실패합니다.  
  
 클래식 모드 로그인을 사용하지 않는 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 웹 서비스에서 처리되는 다음과 같은 유형의 요청은 실패합니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대해 팜의 외부에서 시작된 모든 요청(예: 보고서 디자이너 또는 보고서 작성기에서 데이터 원본으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 대한 SharePoint URL을 참조하는 보고서 작성)  
  
-   외부 데이터 원본으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 사용하는 보고서 또는 클라이언트 응용 프로그램의 팜 내부 요청(예: 두 번째 게시된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 포함 Excel 통합 문서로 데이터 원본을 사용하여 Excel 데스크톱 응용 프로그램에서 통합 문서 작성)  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>응용 프로그램의 인증 공급자를 확인하는 방법  
 새 웹 응용 프로그램을 만들 경우에는 새 웹 응용 프로그램 만들기 페이지에서 **클래식 모드 인증** 옵션을 선택해야 합니다.  
  
 기존 웹 응용 프로그램의 경우 다음 지침에 따라 웹 응용 프로그램이 Windows 인증을 사용하도록 구성되어 있는지 확인합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **웹 응용 프로그램 관리**를 클릭합니다.  
  
2.  웹 응용 프로그램을 선택합니다.  
  
3.  **인증 공급자**를 클릭합니다.  
  
4.  각 영역에 대해 공급자가 하나씩 있고 기본 영역이 Windows로 설정되었는지 확인합니다.  
  
##  <a name="UserConnections"></a> 사용자 권한 부여를 요구하는 Power Pivot 작업  
 SharePoint 인증은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 쿼리 및 데이터 처리에 대한 모든 수준의 액세스에 독점적으로 사용됩니다.  
  
 Analysis Services 역할 기반 권한 부여 모델은 지원되지 않습니다. 셀, 행 또는 테이블 수준에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 역할 기준 권한이 부여되지 않습니다. 따라서 통합 문서의 여러 부분에 각각 보안을 설정하여 특정 사용자에게 해당 부분에 포함된 중요 데이터에 대한 액세스를 허용하거나 거부할 수 없습니다. 포함된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터는 모두 SharePoint 라이브러리의 Excel 통합 문서에 대해 보기 권한이 있는 사용자가 사용할 수 있습니다.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 은 SharePoint 사용자를 가장합니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스에 대한 데이터 연결이 있는 피벗 테이블 또는 피벗 차트를 쿼리하는 경우. 이 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램은 사용자를 대신하여 데이터를 처리하는 특정 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 공유 서비스 인스턴스에 대한 연결을 설정합니다.  
  
-   사용 가능한 데이터가 없을 때 캐시 또는 라이브러리에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 로드하는 경우. 시스템에 아직 로드되지 않은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 데이터 연결 요청이 이루어지면 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스에서 SharePoint 사용자 ID를 사용하여 콘텐츠 라이브러리에서 데이터 원본을 검색한 후 메모리로 로드합니다.  
  
-   데이터 원본의 업데이트된 복사본을 콘텐츠 라이브러리의 통합 문서에 저장하는 데이터 새로 고침 작업을 수행하는 경우. 이 경우 실제 로그온 작업은 Secure Store Service의 대상 응용 프로그램에서 검색되는 사용자 이름과 암호를 사용하여 수행됩니다. 자격 증명은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 무인 데이터 새로 고침 계정이거나 만들 때 데이터 새로 고침 일정에 함께 저장된 자격 증명일 수 있습니다. 자세한 내용은 [파워 피벗 데이터 새로 고침을 위한 저장된 자격 증명 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75) 및 [파워 피벗 무인 데이터 새로 고침 계정 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)을 참조하세요.  
  
##  <a name="Permissions"></a> Power Pivot 데이터 액세스에 대한 SharePoint 사용 권한  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 게시, 관리 및 보안은 SharePoint 통합을 통해서만 지원됩니다. SharePoint 서버에서는 데이터에 대한 합법적인 액세스를 보장하는 인증 및 권한 부여 하위 시스템을 제공합니다. SharePoint 팜 외부에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 안전하게 배포할 수 있는 시나리오는 지원되지 않습니다.  
  
 서버에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 액세스는 보기 이상의 권한을 보유한 사용자에게 읽기 전용으로 제공됩니다. 참가 권한이 있으면 파일을 추가 및 편집할 수 있습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 변경하려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel이 설치된 Excel 데스크톱 응용 프로그램으로 통합 문서를 다운로드해야 합니다. 파일에 대한 참가 권한이 있는 사용자는 파일을 로컬로 다운로드하여 수정한 다음 SharePoint에 다시 저장할 수 있습니다.  
  
 따라서 권한에 대한 참가 및 보기만 수준에 따라 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 유효한 사용자 액세스 권한 집합이 정의됩니다. 기타 권한 수준은 참가 및 보기만과 동일한 사용 권한을 가진 정도로 동작합니다. 예를 들어 읽기 권한에는 보기만 권한이 포함되므로 읽기 권한이 지정된 사용자는 보기만과 동일한 수준의 액세스 권한을 가집니다.  
  
 다음 표는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 및 서버 작업에 대한 액세스 권한을 결정하는 사용 권한 수준을 요약한 것입니다.  
  
|사용 권한 수준|허용되는 태스크|  
|----------------------|------------------------|  
|팜 또는 서비스 관리자|서비스 및 응용 프로그램 설치, 설정 및 구성<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드 사용 및 관리 보고서 보기|  
|모든 권한|사이트 모음 수준에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능 통합 활성화<br /><br /> [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리 라이브러리 만들기<br /><br /> 데이터 피드 라이브러리 만들기|  
|참가|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 추가, 편집, 삭제 및 다운로드<br /><br /> 데이터 새로 고침 구성<br /><br /> SharePoint 사이트에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 기반으로 새 통합 문서 및 보고서 만들기<br /><br /> 데이터 피드 라이브러리에서 데이터 서비스 문서 만들기|  
|읽기|외부 데이터 원본으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 액세스(통합 문서 URL은 Excel의 데이터 연결 마법사와 같은 연결 대화 상자에서 명시적으로 입력)|  
|보기만|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 보기<br /><br /> 데이터 새로 고침 기록 보기<br /><br /> 로컬 통합 문서를 SharePoint 사이트의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 연결하여 해당 데이터를 다른 방식으로 용도 변경<br /><br /> 통합 문서의 스냅숏 다운로드. 스냅숏은 데이터의 정적 복사본이며 슬라이서, 필터, 수식 또는 데이터 연결을 포함하지 않습니다. 스냅숏의 콘텐츠는 브라우저 창에서 셀 값을 복사할 때와 비슷합니다.|  
  
##  <a name="excel"></a> Excel 서비스 보안 고려 사항: Power Pivot 통합 문서  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 쪽 쿼리는 Excel Services와 매우 밀접하게 연관되어 있습니다. 제품 통합은 문서 수준에서 시작되며 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 포함하거나 참조하는 Excel 통합 문서 파일(.xlsx)입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 대해서는 별도의 파일 확장명이 없습니다.  
  
 SharePoint 사이트에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 연 경우 Excel 서비스는 포함된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 연결 문자열을 읽어서 해당 요청을 로컬 SQL Server Analysis Services OLE DB 공급자로 전달합니다. 그러면 공급자는 연결 정보를 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버로 전달합니다. 두 서버 간에 요청이 원활하게 전달되려면 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에 필요한 설정을 사용하도록 Excel 서비스를 구성해야 합니다.  
  
 Excel 서비스에서 보안 관련 구성 설정은 신뢰할 수 있는 위치, 신뢰할 수 있는 데이터 공급자 및 신뢰할 수 있는 데이터 연결 라이브러리에서 지정됩니다. 다음 표에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 액세스를 허용하거나 개선하는 설정에 대해 설명합니다. 아래에 나와 있지 않은 설정은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버 연결에 영향을 주지 않습니다. 이러한 설정을 단계별로 지정하는 방법에 대한 자세한 내용은 [초기 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)에서 "Excel Services 사용" 섹션을 참조하세요.  
  
> [!NOTE]  
>  대부분의 보안 관련 설정은 신뢰할 수 있는 위치에 적용됩니다. 기본값을 유지하거나 다른 사이트에 대해 각각 다른 값을 사용하려는 경우에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터가 포함된 사이트에 추가로 신뢰할 수 있는 위치를 만든 다음 해당 사이트에만 다음 설정을 구성할 수 있습니다. 자세한 내용은 [파워 피벗 사이트에 대한 신뢰할 수 있는 위치 만들기](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)을 참조하세요.  
  
|영역|설정|Description|  
|----------|-------------|-----------------|  
|웹 응용 프로그램|Windows 인증 공급자|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 Excel 서비스에서 가져오는 클레임 토큰을 Windows 사용자 ID로 변환합니다. Excel 서비스를 리소스로 사용하는 웹 응용 프로그램은 Windows 인증 공급자를 사용하도록 구성해야 합니다.|  
|신뢰할 수 있는 위치|위치 유형|이 값은 **Microsoft SharePoint Foundation**으로 설정해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버는 .xlsx 파일의 복사본을 검색하여 팜의 Analysis Services 서버에 로드합니다. 서버는 콘텐츠 라이브러리에서 .xlsx 파일만 검색할 수 있습니다.|  
||외부 데이터 허용|이 값은 **신뢰할 수 있는 데이터 연결 라이브러리 및 포함 라이브러리**로 설정해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 연결은 통합 문서에 포함됩니다. 포함된 연결을 허용하지 않을 경우 사용자는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 캐시를 볼 수 있지만 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터와 상호 작용할 수는 없습니다.|  
||새로 고칠 때 경고|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리를 사용하여 통합 문서 및 보고서를 저장하는 경우 이 값을 사용하지 않도록 설정해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리에는 열 때마다 새로 고침 및 새로 고칠 때 경고가 모두 해제되어 있을 경우 가장 잘 작동하는 문서 미리 보기 기능이 있습니다.|  
|신뢰할 수 있는 데이터 공급자|MSOLAP.4<br /><br /> MSOLAP.5|MSOLAP.4는 기본적으로 포함되지만 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 액세스하려면 MSOLAP.4 공급자가 SQL Server 2008 R2 버전이어야 합니다.<br /><br /> MSOLAP.5는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 과 함께 설치됩니다.<br /><br /> 신뢰할 수 있는 데이터 공급자 목록에서 이 공급자를 제거하지 마십시오. 경우에 따라 팜의 다른 SharePoint 서버에 이 공급자에 대한 복사본을 추가로 설치해야 할 수도 있습니다. 자세한 내용은 [Install the Analysis Services OLE DB Provider on SharePoint Servers](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)을 참조하세요.|  
|신뢰할 수 있는 데이터 연결 라이브러리|(선택 사항)|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 Office 데이터 연결 파일(.odc)을 사용할 수 있습니다. .odc 파일을 사용하여 로컬 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 연결 정보를 제공할 경우 동일한 .odc 파일을 이 라이브러리에 추가할 수 있습니다.|  
|사용자 정의 함수 어셈블리|이 오류에는 이 작업을 적용할 수 없습니다.|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint용 PowerPivot은 Excel Services용으로 빌드하고 배포하는 사용자 정의 함수 어셈블리를 무시합니다. 특정 동작에 대해 사용자 정의 어셈블리를 사용해야 할 경우에도 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 쿼리는 사용자 정의 함수를 사용하지 않고 처리됩니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Power Pivot 서비스 계정 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [파워 피벗 구성 무인된 데이터 새로 고침 계정 (SharePoint 용 파워 피벗)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)   
 [파워 피벗 사이트에 대한 신뢰할 수 있는 위치 만들기](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [Power Pivot 보안 아키텍처](http://go.microsoft.com/fwlink/?linkID=220970)  
  
  
