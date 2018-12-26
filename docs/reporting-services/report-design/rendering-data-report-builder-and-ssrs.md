---
title: 데이터 렌더링(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a458fdf9-fb2a-4fee-9fbd-b38f36e91753
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4be086fc974ccb6338f75eed0cf10ccb0087edc0
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031688"
---
# <a name="rendering-data-report-builder-and-ssrs"></a>데이터 렌더링(보고서 작성기 및 SSRS)
  HTML, MHTML, Word, Excel, PDF 또는 이미지와 같은 레이아웃 렌더러를 사용하면 데이터 및 해당 구성은 변경되지 않습니다. CSV(쉼표로 구분된 값) 또는 XML과 같은 데이터 렌더러 형식을 사용하여 내보내면 시각적 레이아웃 요소는 렌더링되지 않습니다. CSV 및 XML에서는 보고서를 렌더링할 때 보고서 본문 및 해당 내용에 특정 규칙을 적용합니다. 이러한 규칙은 데이터가 해당 형식으로 렌더링되는 방법을 결정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 다음과 같은 작업을 위해 데이터 렌더러를 사용할 수 있습니다.  
  
-   데이터베이스로 가져오기. CSV는 SQL Server 및 Microsoft Access를 비롯한 많은 데이터베이스 애플리케이션에서 쉽게 가져올 수 있는 일반적인 형식입니다.  
  
-   Excel로 가져오기. CSV 렌더러를 사용하여 시각적 레이아웃을 포함하지 않고 데이터를 Excel로 내보낼 수 있습니다. 데이터가 Excel 형식이 되면 차트, 수식 및 피벗 테이블과 같은 표준 Excel 도구를 이용할 수 있습니다.  
  
-   XSLT 변환. XSLT를 XML 렌더러의 출력에 적용할 수 있습니다. 이 서버 측 변환은 데이터를 어떤 형식으로든 변환할 수 있는 강력한 기술입니다.  
  
-   데이터 교환/EDI. 외부 프로세스가 보고서의 CSV 또는 XML 렌더링을 요청한 다음 해당 데이터를 소비할 수 있습니다.  
  
 데이터 렌더러 형식은 레이아웃 렌더러와는 다른 속성 집합에 의해 제어됩니다. 다음은 **속성** 창에서 설정되는 속성 중 데이터 렌더러에만 적용되는 속성의 목록입니다.  
  
-   DataElementOutput 속성은 데이터를 내보낼 때 특정 항목을 데이터에 포함할지 여부를 제어합니다.  
  
-   DataElementName 속성은 데이터 요소의 이름을 제어합니다. CSV에서 이 속성은 CSV 열 머리글의 이름을 제어합니다. XML에서 이 속성은 해당 항목의 XML 요소 또는 특성 이름이 됩니다.  
  
-   DataElementStyle 속성은 XML에서 보고서 항목이 요소와 특성 중 어느 것으로 렌더링될지 제어합니다.  
  
 CSV 내보내기 옵션은 보고서 데이터를 서식 없이 쉼표로 구분된 일반 텍스트 파일로 저장합니다. 기본적으로 이 파일에서는 쉼표(,)를 사용하여 필드 및 행을 구분하지만 이 설정은 디바이스 정보 설정을 사용하여 구성할 수 있습니다. 결과 파일은 Office SharePoint Server와 같은 스프레드시트 프로그램에서 열거나 다른 프로그램의 가져오기 형식으로 사용할 수 있습니다. .csv 파일은 메모장과 같은 텍스트 편집기로 열 수 있습니다. URL로 액세스한 경우 .csv 파일은 **text/csv**의 MIME 형식을 반환합니다. 파일은 MIME 버전 1.0입니다. 보고서를 CSV 파일 형식으로 렌더링하는 방법에 대한 자세한 내용은 [CSV 파일로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)를 참조하세요.  
  
 보고서 데이터 XML 파일 내보내기 옵션은 보고서를 XML 파일로 저장합니다. 보고서의 XML 스키마는 해당 보고서에만 적용됩니다. XML 내보내기 옵션에서 보고서 레이아웃 정보는 저장되지 않습니다. 이 옵션으로 생성된 XML을 데이터베이스로 가져오거나 XML 데이터 메시지로 사용하거나 사용자 지정 애플리케이션에 전송할 수 있습니다. 보고서를 XML 파일 형식으로 렌더링하는 방법에 대한 자세한 내용은 [XML로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Reporting Services 장치 정보 설정(Reporting Services Device Information Settings)](https://go.microsoft.com/fwlink/?LinkId=102515)  
  
  
