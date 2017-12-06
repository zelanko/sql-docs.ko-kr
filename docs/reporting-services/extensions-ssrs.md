---
title: "확장 프로그램(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2bb0fdca-1837-49f5-b542-61826bab0b46
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 90ac80211acb0f761963b1da4889d5319158375e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="extensions-ssrs"></a>확장 프로그램(SSRS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 의 보고서 서버는 받는 입력 또는 출력 유형을 인증, 데이터 처리, 보고서 렌더링, 보고서 배달을 위해 모듈화하는 확장 프로그램을 사용합니다. 이 기능 덕분에 기존 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설치에서 업계의 새 소프트웨어 표준(예: 새 인증 체계 또는 사용자 지정 데이터 원본 유형)을 손쉽게 활용할 수 있습니다. 보고서 서버는 사용자 지정 인증 확장 프로그램, 데이터 처리 확장 프로그램, 보고서 처리 확장 프로그램, 렌더링 확장 프로그램, 배달 확장 프로그램 및 RSReportServer.config 구성 파일에서 사용자가 구성할 수 있는 확장 프로그램을 지원합니다. 예를 들어, 보고서 뷰어에서 사용할 수 있는 내보내기 형식을 제한할 수 있습니다. 보고서 서버는 하나 이상의 인증 확장 프로그램, 데이터 처리 확장 프로그램 및 렌더링 확장 프로그램을 필요로 합니다. 배달 및 보고서 처리 확장 프로그램은 선택적이지만 보고서 배포 또는 사용자 지정 컨트롤을 지원하려는 경우에는 반드시 필요합니다.  
  
 이 항목에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서 사용할 수 있는 확장 프로그램에 대해 설명합니다.  
  
## <a name="security-extensions"></a>보안 확장 프로그램  
 보안 확장 프로그램은 사용자 및 그룹을 인증하고 보고서 서버에 대한 권한을 부여하는 데 사용됩니다. 기본 보안 확장 프로그램은 Windows 인증을 기반으로 합니다. 배포 모델이 다른 인증 접근 방법을 필요로 할 경우(예: 인터넷 또는 엑스트라넷 배포를 위해 폼 기반 인증이 필요한 경우) 기본 보안을 대신하는 사용자 지정 보안 확장 프로그램을 만들 수도 있습니다. 단일 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 설치에서 보안 확장 프로그램은 하나만 사용할 수 있습니다. 기본 Windows 인증 보안 확장 프로그램을 바꿀 수 있지만 사용자 지정 보안 확장 프로그램과 함께 사용할 수는 없습니다.  
  
## <a name="data-processing-extensions"></a>데이터 처리 확장 프로그램  
 데이터 처리 확장 프로그램은 데이터 원본을 쿼리하고 평면화된 행 집합을 반환하는 데 사용됩니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에서는 여러 확장 프로그램을 사용하여 서로 다른 유형의 데이터 원본과 상호 작용합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에 포함된 확장 프로그램을 사용하거나 확장 프로그램을 직접 개발할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)], Hyperion Essbase, Teradata, OLE DB 및 ODBC 데이터 원본에 대한 데이터 처리 확장 프로그램이 제공됩니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 모든 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 데이터 공급자를 사용할 수 있습니다. 데이터 처리 확장 프로그램은 다음 태스크를 수행하여 보고서 처리기 구성 요소의 쿼리 요청을 처리합니다.  
  
-   데이터 원본에 연결합니다.  
  
-   쿼리를 분석하고 필드 이름 목록을 반환합니다.  
  
-   데이터 원본에 대한 쿼리를 실행하고 행 집합을 반환합니다.  
  
-   필요한 경우 매개 변수를 쿼리에 전달합니다.  
  
-   행 집합을 반복 처리하고 데이터를 검색합니다.  
  
 일부 확장 프로그램으로 다음 태스크를 수행할 수도 있습니다.  
  
-   쿼리를 분석하고 쿼리에 사용된 매개 변수 이름 목록을 반환합니다.  
  
-   쿼리를 분석하고 그룹화에 사용된 필드 목록을 반환합니다.  
  
-   쿼리를 분석하고 정렬에 사용된 필드 목록을 반환합니다.  
  
-   사용자 이름과 암호를 제공하여 데이터 원본에 연결합니다.  
  
-   값이 여러 개인 매개 변수를 쿼리에 전달합니다.  
  
-   행을 반복 처리하고 보조 메타데이터를 검색합니다.  
  
## <a name="rendering-extensions"></a>렌더링 확장 프로그램  
 렌더링 확장 프로그램은 보고서 처리기의 데이터 및 레이아웃 정보를 장치 특정 형식으로 변환합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에는 HTML, Excel, CSV, XML, 이미지, PDF 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] 단어의 7개 렌더링 확장 프로그램이 포함되어 입습니다.  
  
-   **HTML 렌더링 확장 프로그램** 웹 브라우저를 통해 보고서 서버에서 보고서를 요청할 때 보고서 서버는 HTML 렌더링 확장 프로그램을 사용하여 보고서를 렌더링합니다. HTML 렌더링 확장 프로그램은 UTF-8 인코딩을 사용하여 모든 HTML을 생성합니다. 자세한 내용은 [HTML로 렌더링&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md) 및 [Reporting Services 및 파워 뷰에 대한 브라우저 지원](../reporting-services/browser-support-for-reporting-services-and-power-view.md)을 참조하세요.  
  
-   **Excel 렌더링 확장 프로그램** Excel 렌더링 확장 프로그램은 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 이상에서 보고 수정할 수 있는 보고서를 렌더링합니다. 이 렌더링 확장 프로그램은 BIFF(Binary Interchange File Format) 파일을 만듭니다. BIFF는 Excel 데이터에 대한 네이티브 파일 형식입니다. [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 에서 렌더링한 보고서는 스프레드시트에서 사용할 수 있는 모든 기능을 지원합니다. 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **CSV 렌더링 확장 프로그램** CSV(쉼표로 구분된 값) 렌더링 확장 프로그램은 보고서를 서식 없이 쉼표로 구분된 일반 텍스트 파일로 렌더링합니다. 그러면 사용자가 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]과 같은 스프레드시트 응용 프로그램이나 텍스트 파일을 읽을 수 있는 다른 프로그램에서 이런 파일을 열 수 있습니다. 자세한 내용은 [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **XML 렌더링 확장 프로그램** XML 렌더링 확장 프로그램은 보고서를 XML 파일로 렌더링합니다. 이렇게 렌더링된 XML 파일은 다른 프로그램에서 읽거나 저장할 수 있습니다. XSLT 변환을 사용하여 보고서를 다른 응용 프로그램에서 사용할 수 있는 다른 XML 스키마로 변환할 수도 있습니다. XML 렌더링 확장 프로그램에서 생성한 XML은 UTF-8로 인코딩됩니다. 자세한 내용은 [XML로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **이미지 렌더링 확장 프로그램** 이미지 렌더링 확장 프로그램은 보고서를 비트맵이나 메타파일로 렌더링합니다. 이 확장 프로그램으로 보고서를 BMP, EMF, GIF, JPEG, PNG, TIFF 및 WMF 형식으로 렌더링할 수 있습니다. 기본적으로 이미지는 TIFF 형식으로 렌더링됩니다. 이 형식은 Windows 사진 및 팩스 뷰어와 같은 운영 체제의 기본 이미지 뷰어로 표시할 수 있습니다. 이미지를 뷰어에서 프린터로 보낼 수 있습니다. 이미지 렌더링 확장 프로그램을 사용하여 보고서를 렌더링하면 보고서가 모든 클라이언트에 동일하게 나타납니다. 예를 들어 보고서를 HTML로 보면 사용자의 브라우저 버전, 브라우저 설정 및 사용 가능한 글꼴에 따라 보고서 모양이 달라질 수 있습니다. 이미지 렌더링 확장 프로그램은 서버에서 보고서를 렌더링하므로 모든 사용자에게 이미지가 동일하게 표시됩니다. 보고서가 서버에서 렌더링되므로 보고서에 사용된 모든 글꼴이 서버에 설치되어 있어야 합니다. 자세한 내용은 [이미지 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **PDF 렌더링 확장 프로그램** PDF 렌더링 확장 프로그램은 보고서를 Adobe Acrobat 6.0 이상에서 열어 볼 수 있는 PDF 파일로 렌더링합니다. 자세한 내용은 [PDF 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)를 참조하세요.  
  
-   **Word 렌더링 확장 프로그램**   [!INCLUDE[msCoName](../includes/msconame-md.md)] Word 렌더링 확장 프로그램은 보고서를 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 이상 버전과 호환되는 Word 문서로 렌더링합니다. 자세한 내용은 [Microsoft Word로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="report-processing-extensions"></a>보고서 처리 확장 프로그램  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에 포함되어 있지 않은 보고서 항목에 대한 사용자 지정 보고서 처리를 제공하도록 보고서 처리 확장 프로그램을 추가할 수 있습니다. 기본적으로 보고서 서버는 표, 차트, 행렬, 목록, 입력란, 이미지 및 기타 보고서 항목을 모두 처리할 수 있습니다. 보고서 실행 중에 사용자 지정 처리를 필요로 하는 보고서에 특수 기능을 추가하려면(예: 보고서에 [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint 맵 포함) 이러한 작업을 수행하는 보고서 처리 확장 프로그램을 만들 수 있습니다.  
  
## <a name="delivery-extensions"></a>배달 확장 프로그램  
 백그라운드 처리 응용 프로그램에서는 배달 확장 프로그램을 사용하여 보고서를 여러 위치에 배치합니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에는 메일 배달 확장 프로그램 및 파일 공유 배달 확장 프로그램이 포함되어 있습니다. 전자 메일 배달 확장 프로그램은 SMTP(Simple Mail Transport Protocol)를 통해 보고서 자체 또는 보고서 URL 링크가 들어 있는 전자 메일 메시지를 보냅니다. URL 링크 또는 보고서가 없는 간단한 알림은 호출기, 전화 또는 기타 장치로 보낼 수 있습니다. 파일 공유 배달 확장 프로그램은 네트워크의 공유 폴더에 보고서를 저장합니다. 사용자가 만든 파일의 위치, 렌더링 형식, 파일 이름 및 덮어쓰기 옵션을 지정할 수 있습니다. 파일 공유 배달은 렌더링한 보고서의 보관 및 대용량의 보고서 작업을 위한 전략의 일환으로 사용할 수 있습니다. 배달 확장 프로그램은 구독과 함께 사용됩니다. 구독을 만들 때 사용자는 사용할 수 있는 배달 확장 프로그램을 선택하여 보고서 배달 방법을 결정할 수 있습니다.  
  
  
