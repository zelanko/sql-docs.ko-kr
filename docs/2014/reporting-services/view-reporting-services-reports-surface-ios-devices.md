---
title: Microsoft Surface 장치 및 Apple iOS 장치에서 Reporting Services 보고서 보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- iPad
- Safari
- SSRS
- Report Viewer [Reporting Services]
- iOS
ms.assetid: 2124bcf5-d60a-475f-a4ae-de6df44d2860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ca879d51f947ec078b3c1b7e14842ea926f0240
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174852"
---
# <a name="view-reporting-services-reports-on-microsoft-surface-devices-and--apple-ios-devices"></a>Microsoft Surface 디바이스 및 Apple iOS 디바이스에서 Reporting Services 보고서 보기
  이 문서에서는 Microsoft Surface 디바이스 및 iPad와 같은 Apple iOS 6 및 Apple Safari 디바이스에서 지원되는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 기능 및 워크플로를 설명합니다.

## <a name="view-and-interact-with-reports"></a>보고서 보기 및 상호 작용
 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]부터 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 Microsoft Surface 디바이스 및 iPad와 같은 Apple iOS 6 및 Apple Safari 브라우저 디바이스에서 보고서 보기 및 기본 상호 작용을 지원합니다. Microsoft Surface 디바이스를 사용하는 보고서를 게시할 수도 있습니다.

 ![IPad 데스크톱](media/videothumbnail.jpg "IPad 바탕 화면") IPad에서 보고서를 보는 방법에 대 한 데모를 시청 하세요.

 Windows Phone 8 디바이스에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서를 볼 수도 있습니다.

 이 항목에서 설명하는 기능을 활용하려면 다음 중 하나를 설치하세요.

-   기본 모드 보고서 서버의 경우 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] 이상을 설치하세요.

     [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]는 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=35575)에서 다운로드할 수 있습니다.

-   SharePoint 모드 보고서 서버의 경우 SharePoint 제품용 [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] 추가 기능( [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 이상)을 설치하세요.

 **iPad 디바이스 또는 Microsoft Surface 디바이스에서 보고서를 보고 상호 작용하려면**

1.  보고서 서버 또는 보고서가 있는 SharePoint 사이트에 연결할 수 있는지 확인합니다.

2.  다음 중 하나를 수행하여 보고서를 엽니다.

    -   **전자 메일에서 시작:**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 구독으로 만들어진 전자 메일에서 보고서의 URL을 탭합니다. 보고서가 브라우저에서 열립니다.

    -   **보고서 서버에서 시작:**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버에 있는 디렉터리를 찾은 다음 보고서 이름을 탭하여 보고서를 엽니다.

    -   **SharePoint 문서 라이브러리에서 시작:**[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서가 포함된 SharePoint 문서 라이브러리를 찾은 다음 보고서 이름을 탭합니다. 보고서를 보고 상호 작용할 수 있습니다.

        > [!IMPORTANT]
        >  iPad의 경우 Safari의 **Private 브라우징** 속성이 해제되어 있는지 확인합니다.

    -   **SharePoint 웹 파트:** SharePoint 페이지에 웹 파트가 추가된 경우 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서를 볼 수 있습니다.

3.  Microsoft Surface 디바이스에서 보고서 관리자를 사용하여 보고서를 열 수도 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 관리자에 있는 디렉터리를 찾은 다음 보고서 이름을 눌러 보고서를 엽니다.

    > [!IMPORTANT]
    >  보고서 관리자에서 보고서 보기는 iPad에서 지원되지 않습니다.

4.  다음과 같은 방법으로 스크롤 및 확대/축소합니다.

    -   보고서를 스크롤하려면 스크린에서 위쪽, 아래쪽, 왼쪽 또는 오른쪽으로 손가락을 끕니다. 살짝 밀기입니다.

    -   확대하려면 화면에 두 손가락을 놓고 손가락 사이를 벌립니다. 축소하려면 화면에 두 손가락을 놓고 손가락 사이를 좁힙니다. 축소 제스처입니다.

5.  다음과 같은 방법으로 보고서를 탐색하고 상호작용합니다.

    -   축소하려면 더하기 기호(+)를 누르고 확장하려면 빼기 기호(-)를 눌러 그룹과 관련된 행과 열 및 보고서 항목을 축소하고 확장합니다.

    -   정렬 단추를 눌러 행렬의 행과 열 또는 테이블 행의 순서를 오름차순이나 내림차순으로 설정/해제합니다. 정렬 단추는 일반적으로 열 머리글에 위치합니다.

    -   보고서 위쪽의 화살표 단추를 눌러 매개 변수 창을 확장하고 축소합니다.

    -   매개 변수 옆에 있는 상자 또는 컨트롤을 눌러 매개 변수 값을 선택합니다. **보고서 보기** 를 눌러 보고서에 매개 변수 값을 적용합니다.

    -   **찾기** 옆에 있는 상자를 눌러 검색 용어를 입력한 다음 **찾기**를 눌러 보고서 내용을 검색합니다.

    -   탐색 단추를 누르거나 단추 옆 입력란을 누르고 페이지 번호를 입력하여 보고서 페이지를 탐색합니다.

    -   텍스트 상자, 이미지, 차트 및 계기와 같은 보고서 항목에 추가된 하이퍼링크를 눌러 URL로 이동합니다.

    -   **드롭다운 메뉴 내보내기** 아이콘을 누른 다음 파일 형식을 눌러서 보고서를 내보냅니다.

        -   Microsoft Surface 장치에서 보고서를 보는 경우 다음 형식 중 하나로 보고서를 내보낼 수 있습니다.

            -   보고서 데이터를 가진 XML 파일

            -   CSV(쉼표로 분리)

            -   PDF

            -   MHTML(웹 보관 파일)

            -   Excel

            -   TIFF

            -   Word

        -   IPad에서 보고서를 볼 때 보고서를 TIFF 또는 PDF 파일로 내보낼 수 있습니다.

## <a name="authentication"></a>인증
 RSWindowsNTLM 인증 및 RSWindowsBasic 인증은 기본 모드 및 iPad에서 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 와 작동합니다.

 일반적으로 RSWindowsBasic은 인증 유형이 전송된 자격 증명에 대한 기밀성을 제공하지 않기 때문에 https가 아닌 환경에서 사용하지 않는 것이 좋습니다.

 RSWindowsNTLM 및 RSWindowsBasic 인증에 대한 자세한 내용은 [Authentication with the Report Server](security/authentication-with-the-report-server.md)을 참조하세요.

## <a name="uploading-reports"></a>보고서 업로드
 적절한 권한이 있는 경우 다음 방법 중 하나를 사용하여 Microsoft Surface 디바이스에서 보고서를 게시할 수 있습니다.

> [!IMPORTANT]
>  이러한 방법은 iPad에서 지원되지 않습니다.

-   라이브러리를 열고 **문서 업로드**를 눌러 SharePoint 문서 라이브러리에 보고서 정의 파일(.rdl)을 업로드합니다.

-   보고서 관리자를 열고 **파일 업로드**를 눌러 보고서 서버 데이터베이스에 보고서 정의 파일을 업로드합니다.

## <a name="additional-information"></a>추가 정보
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 및 지원되는 브라우저에 대한 자세한 내용은 다음을 참조하세요.

-   [Reporting Services 및 파워 뷰 브라우저 지원 계획 &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)

 Microsoft Business Intelligence 및 모바일 디바이스에 대한 자세한 내용을 다음을 참조하세요.

-   [모바일 장치 및 SharePoint 2013 개요](https://technet.microsoft.com/library/fp161351\(v=office.15\).aspx) (https://technet.microsoft.com/library/fp161351(v=office.15).aspx).

-   [SharePoint 2013에서 지원 되는 모바일 장치 브라우저](https://technet.microsoft.com/library/fp161353\(v=office.15\).aspx) (https://technet.microsoft.com/library/fp161353(v=office.15).aspx).

-   [Apple iPad 장치에서 보고서 및 성과 기록표 보기 (SharePoint Server 2010)](https://technet.microsoft.com/library/hh697482.aspx) (https://technet.microsoft.com/library/hh697482.aspx).

-   [IPad에서 Reporting Services 보고서 보기 (비디오) ()](https://technet.microsoft.com/sqlserver/jj873792.aspx) https://technet.microsoft.com/sqlserver/jj873792.aspx)

-   [Microsoft Surface RT 디바이스에서 Reporting Services 보고서 보기(비디오)](https://technet.microsoft.com/sqlserver/dn146017)


