---
title: Excel에서 BI 의미 체계 모델 연결을 사용 하거나 Reporting Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f7141cb88a69df946fc7ae1d344cf0a2723bd7c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="use-a-bi-semantic-model-connection-in-excel-or-reporting-services"></a>Excel 또는 Reporting Services에서 BI 의미 체계 모델 연결 사용
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  이 항목에서는 다른 항목의 지침을 사용하여 만든 BI 의미 체계 모델 연결을 사용하는 방법에 대해 설명합니다. BI 의미 체계 모델을 만들지 않은 경우 [파워 피벗 통합 문서에 대한 BI 의미 체계 모델 연결 만들기](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md) 및 [테이블 형식 model 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)를 참조하세요.  
  
##  <a name="bkmk_connect"></a> Excel에서 연결  
 Analysis Services 테이블 형식 모델 데이터를 사용하는 다른 비즈니스 응용 프로그램이나 Excel에서 BI 의미 체계 모델 연결을 데이터 원본으로 지정할 수 있습니다. 이 섹션에서는 Excel을 사용하여 BI 의미 체계 모델에 연결하는 두 가지 방법에 대해 설명합니다.  
  
 Excel에서 BI 의미 체계 모델에 연결하려면 워크스테이션에 Excel 2010 및 MSOLAP.5 OLE DB Provider가 설치되어 있어야 합니다. 연결 요구 사항에 대한 추가 정보는 이 섹션에서 자세하게 제공합니다.  
  
 **SharePoint에서 시작**  
  
-   라이브러리에서 BI 의미 체계 모델 연결을 마우스 오른쪽 단추로 클릭하고 **Excel 시작**을 선택합니다.  
  
 ![빠른 시작 명령의 스크린 샷의 BISM](../../analysis-services/power-pivot-sharepoint/media/ssas-bism-quicklaunch.gif "스크린 샷의 BISM 빠른 실행 명령")  
  
 데이터 연결을 사용하도록 설정할지를 묻는 메시지가 표시되면 **사용** 을 클릭합니다. 기본 데이터 원본의 필드로 채워진 피벗 테이블 필드 목록이 포함된 통합 문서가 Excel에서 열립니다.  
  
 **Excel에서 시작**  
  
1.  Excel을 시작하고 통합 문서를 엽니다. 데이터 탭의 외부 데이터 가져오기에서 **기타 원본**을 클릭합니다.  
  
2.  **Analysis Services** 를 클릭하고 데이터 연결 마법사를 사용하여 데이터를 가져옵니다.  
  
3.  BI 의미 체계 모델 연결 파일의 SharePoint URL(예: `http://mysharepoint/shared documents/myData.bism`)을 입력합니다. 기본 로그온 자격 증명 옵션인 **Windows 인증 사용**을 사용합니다. **다음**을 클릭합니다.  
  
4.  다음 페이지에서 **다음** 을 다시 클릭합니다. 데이터베이스를 선택하라는 메시지가 표시되지만 BI 의미 체계 모델 연결에 지정된 한 데이터베이스만 사용할 수 있습니다.  
  
5.  마지막 페이지에서 이름 및 설명을 제공할 수 있습니다. **마침**을 클릭하고 데이터 가져오기 대화 상자에서 **확인** 을 클릭하여 데이터를 가져옵니다.  
  
 연결에 성공하려면 Excel 2010 및 MSOLAP.5.dll이 클라이언트 컴퓨터에 설치되어 있어야 합니다. 이 릴리스에 현재 사용할 수 있는 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel을 설치하여 공급자를 얻거나, [기능 팩 다운로드 페이지](http://go.microsoft.com/fwlink/?linkid=214066)에서 Analysis Services OLE DB Provider를 다운로드할 수 있습니다.  
  
 MSOLAP.5.dll이 최신 버전인지 확인하려면 레지스트리에서 **HKEY_CLASSES_ROOT\MSOLAP** 를 확인합니다. **CurVer** 이 MSOLAP.5로 설정되어 있어야 합니다.  
  
 또한 SharePoint에서 BI 의미 체계 모델 파일에 대한 읽기 권한도 있어야 합니다. 읽기 권한에는 다운로드 권한이 포함됩니다. Excel에서는 SharePoint에서 BI 의미 체계 모델 연결 정보를 다운로드하고 **HTTP Get**을 통해 데이터베이스에 직접 연결합니다. BI 의미 체계 모델 연결 정보가 로컬로 저장되면 연결 요청이 SharePoint를 통해 전달되지 않습니다.  
  
 Analysis Services 서버에서 실행되는 테이블 형식 model 데이터베이스에 연결하는 경우 SharePoint 사용 권한이 충분하지 않습니다. 서버에 대한 데이터베이스 읽기 권한도 있어야 합니다. 이 단계는 BI 의미 체계 모델 연결을 만들 때 수행했어야 합니다. 자세한 내용은 [테이블 형식 model 데이터베이스에 대한 BI 의미 체계 모델 연결 만들기](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)를 참조하세요.  
  
##  <a name="bkmk_use"></a> SharePoint의 Reporting Services에서 연결  
 데이터를 사용하는 문서 또는 도구에서 BI 의미 체계 모델 연결 파일을 데이터 원본으로 지정하여 대부분의 데이터 원본을 사용하는 것과 같은 방법으로 BISM 연결을 사용할 수 있습니다. BI 의미 체계 모델 연결이 다른 서버의 실제 데이터베이스를 가리키지만 연결 파일을 데이터 원본인 것처럼 사용합니다. BI 의미 체계 모델 연결의 SharePoint URL은 BI 의미 체계 모델 데이터를 사용하는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 보고서의 유효한 데이터 원본 위치입니다.  
  
 SharePoint에 있는 임시 보고서 디자인의 경우 해당 보고서를 만드는 사용자가 BI 의미 체계 모델 연결(.bism) 파일 및 비즈니스 인텔리전스 의미 체계 model 데이터베이스에 대한 SharePoint 사용 권한을 갖고 있어야 합니다. 연결의 보안 컨텍스트는 보고서를 만들고 있는 대화형 사용자입니다.  
  
  
