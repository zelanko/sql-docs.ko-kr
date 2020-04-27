---
title: SharePoint 모드의 보고서 서버에 게시 된 보고서 항목에 대 한 URL 예 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7cbf3b3e6e378f27e5c56de6b043c95c56774f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099447"
---
# <a name="url-examples-for-published-report-items-on-a-report-server-in-sharepoint-mode-ssrs"></a>SharePoint 모드의 보고서 서버에 게시된 보고서 항목에 대한 URL 예(SSRS)
  SharePoint 라이브러리에 보고서 및 관련 항목을 게시하려면 보고서 디자이너와 같은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 제작 도구를 사용하여 내용을 게시하거나 SharePoint 사이트 동작을 사용하여 내용을 업로드합니다.  
  
 SharePoint 사이트는 기본 모드의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버와는 다른 웹 주소를 사용합니다. SharePoint 사이트 웹 계층에는 SharePoint 웹 애플리케이션, 최상위 사이트, 선택적 하위 사이트 및 라이브러리가 포함됩니다. SharePoint 서버를 지정하는 URL 주소를 만드는 방법과 보고서 또는 관련 항목을 게시할 SharePoint 사이트 계층의 위치를 알아야 합니다.  
  
 보고서 관련 항목에는 공유 데이터 원본, 하위 보고서, 드릴스루 보고서 및 웹 기반 이미지 파일과 같은 리소스가 포함됩니다. SharePoint 라이브러리에 게시된 보고서는 SharePoint 라이브러리에서의 위치에 따라 이러한 관련 항목을 지정해야 합니다.  
  
 이 항목의 예를 사용하면 보고 솔루션에서 보고서 및 관련 항목 URL을 만드는 데 도움이 됩니다.  
  
## <a name="site-hierarchy"></a>사이트 계층  
 SharePoint 통합 모드로 실행되도록 보고서 서버를 구성하면 보고서 서버에서 처리 및 관리되는 항목을 다루는 데 SharePoint 웹 계층이 사용됩니다.  
  
 웹 계층의 다음 요소를 사용하여 보고서 서버 내용에 액세스하고 보안을 유지할 수 있습니다. 목록 및 페이지와 같은 다른 개체는 보고서 서버 내용에 액세스하는 데 사용되지 않으므로 다음 표에서 설명하지 않습니다.  
  
|Object|Description|  
|------------|-----------------|  
|SharePoint 웹 애플리케이션|SharePoint 웹 애플리케이션은 독립 실행형 서버로 설치하거나 가상 서버 컬렉션이 포함된 팜에 설치할 수 있습니다. 웹 애플리케이션에는 URL(예: http:*//servername*)이 있으며 여러 사이트가 포함될 수 있습니다.|  
|사이트|사이트는 웹 애플리케이션의 부모 사이트 또는 하위 사이트입니다.|  
|SharePoint 라이브러리|라이브러리에는 문서나 폴더가 들어 있습니다. 라이브러리 또는 라이브러리 내의 폴더는 보고서, 보고서 모델, 공유 데이터 원본 및 외부 이미지를 저장할 수 있는 유일한 사이트 개체입니다.|  
|항목|URL에서 참조할 수 있는 보고서 서버 항목에는 보고서나 하위 보고서에 대한 보고서 정의, 보고서 모델, 공유 데이터 원본 또는 외부 이미지가 있습니다.|  
  
## <a name="url-syntax-and-rules"></a>URL 구문 및 규칙  
 라이브러리의 각 보고서 서버 항목은 프로토콜 접두사, 서버 이름, 사이트, 라이브러리, 파일 이름 및 파일 유형의 파일 확장명을 포함하는 정규화된 URL로 식별됩니다.  
  
### <a name="url-for-a-sharepoint-server"></a>SharePoint 서버에 대한 URL  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 보고서 서버로 보고서 서버 또는 보고서 모델 프로젝트를 배포하는 경우 SharePoint 서버에 대한 URL을 사용해야 합니다.  
  
 사용할 서버의 이름을 찾으려면 브라우저를 열고 보고서를 게시할 SharePoint 라이브러리를 찾습니다. 서버 이름은 프로토콜 접두사 바로 뒤에 표시됩니다(예: http:*//servername*).  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL 프록시 엔드포인트는 사용할 수 없습니다. 프록시 엔드포인트에는 포트 번호가 포함됩니다(예: http:*//servername:8080/reportserver*).  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>SharePoint 서버 사이트 또는 하위 사이트에 대한 URL  
 보고서 또는 보고서 데이터 원본을 배포하는 경우 SharePoint 사이트 및 하위 사이트(있는 경우)에 대한 URL을 사용해야 합니다. URL에서 사이트 이름은 서버 이름 바로 뒤에 표시됩니다(예: http://*servername/site* 또는 http://*servername/site/subsite*).  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 웹 애플리케이션에서 사이트와 하위 사이트는 주 사이트의 탭에 해당하는 경우가 많습니다. 사이트 이름이나 하위 사이트 이름을 찾으려면 **홈**, **모든 사이트 콘텐츠**를 차례로 클릭합니다. 그런 다음 아래쪽으로 스크롤하여 **사이트 및 작업 영역**을 찾습니다. 이 섹션에 사이트 목록이 표시됩니다.  
  
### <a name="url-for-a-sharepoint-library"></a>SharePoint 라이브러리에 대한 URL  
 SharePoint 라이브러리에 보고서나 관련 항목을 배포하는 경우 SharePoint 라이브러리에 대한 URL을 사용해야 합니다. 라이브러리에 사용할 URL은 사용하는 SharePoint 버전에 따라 달라집니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 또는 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]에서는 라이브러리가 서버 이름 뒤에 표시됩니다(예: http://*servername/* Shared Documents).  
  
 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]에서는 라이브러리가 사이트 및 하위 사이트 뒤에 표시됩니다(예: http://*servername/site/* Documents).  
  
 새 SharePoint 라이브러리나 잘 모르는 사이트의 경로 정보를 찾으려면 브라우저를 열고 보고서를 게시할 SharePoint 라이브러리를 찾습니다. 라이브러리가 비어 있으면 임의의 파일을 업로드합니다. 그런 다음 해당 파일을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하여 **속성** 창을 엽니다. 파일 주소에 게시 작업을 위해 필요한 URL 값이 들어 있습니다.  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>SharePoint 사이트의 항목에 대한 정규화된 URL  
 SharePoint 라이브러리에 저장된 항목의 주소는 항상 루트 노드로 사용되는 웹 애플리케이션으로 시작하여(http://*server*) 참조하는 파일 이름으로 끝나는 정규화된 URL로 지정됩니다.  
  
 URL의 파일 이름에는 파일 확장명이 포함되어야 합니다.  
  
 SharePoint 사이트에 게시하는 보고서에는 종속 항목에 대한 상대 URL을 사용할 수 없습니다. 예를 들어 상대 URL을 사용하여 공유 데이터 원본, 보고서 모델 또는 하위 보고서를 참조할 수 없습니다. 각 항목에 대해 항상 SharePoint 라이브러리에 대한 정규화된 URL을 지정해야 합니다. URL 형식을 구문 분석하는 데 사용할 수 있는 미리 정의된 사이트 계층이 없으므로 가능한 종속 파일 위치를 예측할 수 없습니다.  
  
 종속 항목이 하위 보고서를 게시하거나 업로드하는 경우 보고서가 게시된 후 종속 항목에 대한 참조를 설정해야 합니다. 보고서 디자이너의 미리 보기 모드에서 참조가 제대로 작동했다고 해서 보고서가 게시된 후 항상 참조가 제대로 작동하는 것은 아닙니다. 자세한 내용은 이 항목의 [제작 도구에서 SharePoint 라이브러리로 게시](#publishingToDocLib) 를 참조하십시오.  
  
### <a name="urls-for-external-images"></a>외부 이미지에 대한 URL  
 보고서 정의는 외부 파일로 저장된 이미지 파일을 포함할 수 있습니다. 이미지 파일에 대한 정규화된 URL을 설정하여 보고서 정의에서 해당 파일을 참조할 수 있습니다. 이러한 외부 파일은 SharePoint 사이트나 원격 컴퓨터에 저장될 수 있습니다.  
  
> [!IMPORTANT]  
>  외부 URL이 SharePoint 사이트의 이미지에 대한 URL인 경우 보고서 작성기에서 보고서를 미리 보면 깨진 이미지 아이콘이 표시됩니다. SharePoint 사이트에 보고서를 업로드하고 연결된 모드에서 보고서를 렌더링하는 경우 `View Items` 권한만 있으면 깨진 이미지 아이콘이 표시됩니다.  
  
 보고서 서버 모드에 관계없이 보고서의 외부 이미지에 대한 참조는 정규화된 URL이어야 합니다. 또한 외부 이미지 파일을 참조하는 경우 일반적으로 무인 보고서 처리 계정을 구성해야 합니다.  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>하위 보고서 및 드릴스루 보고서 지정  
 하위 보고서는 주 보고서와 같은 폴더에 있어야 합니다. 상대 폴더는 지정할 수 없습니다.  
  
 드릴스루 보고서를 지정하려면 식에 URL을 포함합니다. 예를 들어 SalesDetails라는 보고서를 드릴스루 보고서로 지정하려면 입력란 또는 자리 표시자 텍스트에 대한 동작에서 ReportName을 다음 식으로 설정합니다.  
  
```  
="http://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>SharePoint 사이트의 예약된 이름  
 SharePoint 사이트에 있는 항목에 대한 URL을 만드는 경우 **Personal** 및 **Sites** 라는 단어는 모두 기본 사이트에 예약된 이름입니다.  
  
## <a name="examples-of-urls"></a>URL의 예  
 SharePoint 라이브러리에 항목을 게시하는 경우 대상 라이브러리에 대한 정규화된 URL을 지정해야 합니다. 정규화된 SharePoint URL에는 SharePoint 웹 애플리케이션, 사이트, 라이브러리, 폴더(옵션), 파일 및 파일 확장명이 포함됩니다. 다음 예에서는 사용해야 하는 몇 가지 구문을 보여 줍니다.  
  
|대상|URL 예|  
|------------|-----------------|  
|SharePoint 서버|http://TestServer|  
|SharePoint 서버 사이트 또는 하위 사이트|http://TestServer/toplevelsite/subsite|  
|**또는**[!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 배포의 공유 문서 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 에 있는 Company Sales 예제 보고서|http://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl|  
|**또는** 인스턴스의 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] Documents/Doc [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 폴더에 있는 Company Sales 샘플 보고서|http://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl|  
|**또는**[!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 인스턴스의 보고서 센터 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 에 있는 Company Sales 예제 보고서|http://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl|  
  
##  <a name="publishing-from-an-authoring-tool-to-a-sharepoint-library"></a><a name="publishingToDocLib"></a> 제작 도구에서 SharePoint 라이브러리로 게시  
 보고서 제작 도구를 사용하여 보고서 및 관련 파일을 라이브러리에 게시하는 경우 파일은 추가되기 전에 유효한지 검사됩니다. SharePoint 라이브러리의 **업로드** 동작을 사용하여 보고서 및 관련 파일을 업로드하면 유효성 검사가 수행되지 않습니다. 보고서에 액세스하여 관리, 편집 또는 실행할 때까지 파일이 올바른지 여부를 확인할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SharePoint 사이트로 보고서를 게시하려면 Internet Explorer 브라우저에서 해당 SharePoint 사이트를 신뢰할 수 있는 위치 목록에 추가해야 합니다.  
  
### <a name="shared-data-sources"></a>공유 데이터 원본  
 보고서 제작 도구에서 공유 데이터 원본을 게시하는 경우 프로젝트 속성 `TargetDataSourceFolder`를 설정합니다. 대상 데이터 원본 폴더는 SharePoint 라이브러리에 대한 URL이어야 합니다. 상대 경로는 유효하지 않으므로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드에서와 달리 상대 폴더를 지정할 수 없습니다. 문서 라이브러리 경로의 폴더가 없으면 자동으로 생성됩니다.  
  
 SharePoint 사이트에 공유 데이터 원본 파일(.rds)을 게시하면 데이터 원본 파일의 확장명이 .rsds로 변경됩니다. .rsds 파일은 SharePoint 사이트에서 로컬로 저장할 수 없으며 기존 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 프로젝트로 가져올 수 없습니다. 파일 확장명이 .rds인 공유 데이터 원본과 .rsds인 공유 데이터 원본은 서로 바꿔 사용할 수 없습니다.  
  
#### <a name="shared-data-sources-from-report-designer"></a>보고서 디자이너의 공유 데이터 원본  
 보고서 디자이너 프로젝트에서 공유 데이터 원본을 게시하는 경우 대상 라이브러리를 지정하는 URL을 사용하거나 속성을 비워 둘 수 있습니다. 상대 경로는 유효하지 않으므로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드에서와 달리 상대 폴더를 지정할 수 없습니다. 문서 라이브러리 경로의 폴더가 없으면 자동으로 생성됩니다. 대상 데이터 원본 폴더를 비워 두면 데이터 원본이 대상 보고서 폴더에 게시됩니다.  
  
### <a name="file-names"></a>파일 이름  
 보고서 항목에 대한 URL의 파일 이름에는 파일 확장명이 포함되어야 합니다. 이러한 파일 확장명에 따라 파일 유형이 결정됩니다. 보고서 제작 도구에서 보고서 항목을 게시하는 경우 파일 확장명이 자동으로 포함됩니다. SharePoint 라이브러리에 보고서 항목을 업로드하는 경우에는 파일 확장명을 포함해야 합니다.  
  
 SharePoint 사이트에 업로드하는 항목의 파일 확장명을 지정하지 않으면 `rsInvalidDataSourceReference` 오류가 발생합니다. SharePoint 애플리케이션에서 올바른 파일 이름 문자로 인식하지 않는 문자는 파일 이름에 사용할 수 없습니다. 다음 문자를 포함 하지 마세요. #% & *: \< >? 마십시오.  
  
## <a name="differences-between-uploading-and-publishing"></a>업로드와 게시의 차이점  
 보고서 디자이너 또는 보고서 작성기를 사용하여 보고서 및 관련 파일을 라이브러리에 게시하는 경우 파일이 추가되기 전에 해당 유효성이 검사됩니다. SharePoint 라이브러리의 **업로드** 동작을 사용하여 보고서 및 관련 파일을 업로드하면 유효성 검사가 수행되지 않습니다. 보고서에 액세스하여 관리, 편집 또는 실행할 때까지 파일이 올바른지 여부를 확인할 수 없습니다.  
  
## <a name="updating-a-published-item"></a>게시된 항목 업데이트  
 SharePoint 라이브러리에 항목을 게시하거나 업로드한 후 업데이트하기 전에 라이브러리에서 항목을 체크 아웃해야 합니다. 보고서를 체크 아웃한 사용자만 해당 보고서를 변경할 수 있습니다. 작업이 완료되면 보고서를 다시 체크 인합니다.  
  
 기존 항목과 이름이 같은 항목을 업로드하는 등 먼저 문서를 체크 아웃하지 않고 보고서를 업로드하거나 게시하면 보고서 서버에서 문서를 자동으로 체크 아웃하고 업데이트된 보고서를 기존 항목의 새 버전으로 추가한 다음 문서를 다시 체크 인합니다.  
  
## <a name="external-images-as-resources"></a>리소스로서의 외부 이미지  
 기본 모드로 실행되는 보고서 서버에서 리소스의 개념은 보고서 서버에 저장되고 보안이 유지되지만 보고서 서버에서 처리하지는 않는 임의의 파일을 의미합니다. 기본 모드에서 리소스는 모든 종류의 파일이 될 수 있습니다.  
  
 보고서 서버가 SharePoint 통합 모드로 실행되는 경우에는 리소스의 개념 정의가 보다 좁아집니다. 여기서 리소스는 외부 이미지를 참조하는 보고서를 저장하기 위한 개념입니다. 이 경우 보고서는 내부 사용을 위해 유지되는 복사본이나 스냅샷입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 라이브러리에 보고서 게시](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [SharePoint 라이브러리에 공유 데이터 원본 게시](../reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [프로젝트 속성 페이지 대화 상자](project-property-pages-dialog-box.md)  
  
  
