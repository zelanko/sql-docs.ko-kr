---
title: "(보고서 작성기 및 SSRS) CSV 파일로 내보내기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68ec746e-8c82-47f5-8c3d-dbe403a441e5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 60c8d93cd6901e6a18337212f8906ccbbf0f5522
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="exporting-to-a-csv-file-report-builder-and-ssrs"></a>CSV 파일로 내보내기(보고서 작성기 및 SSRS)
  CSV(쉼표로 구분된 값) 렌더링 확장 프로그램은 페이지가 매겨진 보고서의 데이터를 결합하여 읽기 쉽고 많은 응용 프로그램과 교환할 수 있는 표준화된 일반 텍스트 형식으로 렌더링합니다.  
  
 CSV 렌더링 확장 프로그램에서는 필드와 행을 구분하기 위해 문자열 구분 기호를 사용하는데 이 문자열 구분 기호는 쉼표 이외의 문자로 구성 가능합니다. 결과 파일은 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 과 같은 스프레드시트 프로그램에서 열거나 다른 프로그램의 가져오기 형식으로 사용할 수 있습니다. 내보낸 보고서는 .csv 파일이 되며 **text/csv**MIME 형식을 반환합니다.  
  
 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]의 차트, 데이터 막대, 스파크라인, 계기 및 표시기와 관련된 데이터를 사용하려면 보고서를 CSV 파일로 내보낸 다음 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel에서 이 파일을 엽니다.  
  
 CSV 형식으로 내보내는 방법에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CSVRendering"></a> CSV 렌더링  
 기본 설정을 사용하여 렌더링된 CSV 보고서는 다음과 같은 특징을 가집니다.  
  
-   기본 필드 구분 기호 문자열은 쉼표(,)입니다.  
  
    > [!NOTE]  
    >  장치 정보 설정을 변경하여 필드 구분 기호를 TAB을 비롯한 임의의 문자로 변경할 수 있습니다. 자세한 내용은 [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md)을 참조하세요.  
  
-   레코드 구분 기호 문자열은 캐리지 리턴 및 줄 바꿈 (\<cr >\<lf >).  
  
-   텍스트 한정자 문자열은 인용 부호(")입니다.  
  
     CSV 렌더러는 일부 텍스트 문자열 주위에만 한정자를 추가합니다. 텍스트 한정자는 값에 구분 기호 문자가 포함되어 있거나 값에 줄 바꿈이 있을 때만 추가됩니다.  
  
-   텍스트에 포함 구분 기호 문자열이나 한정자 문자열이 포함되어 있는 경우 텍스트 한정자는 텍스트 양 끝에 놓이며 포함 한정자 문자열은 중복됩니다.  
  
-   서식 및 레이아웃은 무시됩니다.  
  
 렌더링하는 동안 다음 항목은 무시됩니다.  
  
-   페이지 머리글  
  
-   페이지 바닥글  
  
-   사용자 지정 보고서 항목  
  
-   선  
  
-   이미지  
  
-   사각형  
  
-   자동 부분합  
  
 나머지 보고서 항목은 위쪽에서 아래쪽으로 정렬된 다음 왼쪽에서 오른쪽으로 정렬됩니다. 그런 다음 각 항목이 열로 렌더링됩니다. 보고서에 목록이나 테이블과 같은 중첩된 데이터 항목이 있는 경우 부모 항목이 각 레코드에서 반복됩니다.  
  
 다음 표는 보고서 항목이 렌더링될 때의 모양을 보여 줍니다.  
  
|항목|렌더링 동작|  
|----------|------------------------|  
|입력란|입력란의 내용을 렌더링합니다. 기본 모드에서는 항목의 서식 속성에 따라 항목의 서식이 지정됩니다. 규격 모드에서는 서식이 장치 정보 설정에 의해 변경될 수 있습니다. CSV 렌더링 모드에 대한 자세한 정보는 다음을 참조하십시오.|  
|테이블|테이블을 확장하고 최하위 수준에서 각 행과 열에 대한 행과 열을 만들어 렌더링합니다. 부분합 행과 열에는 열 머리글이나 행 머리글이 없습니다. 드릴스루 보고서는 지원되지 않습니다.|  
|행렬|행렬을 확장하고 최하위 수준에서 각 행과 열에 행과 열을 만들어 렌더링합니다. 부분합 행과 열에는 열 머리글이나 행 머리글이 없습니다.|  
|목록|목록의 각 정보 행이나 인스턴스에 대해 레코드를 렌더링합니다.|  
|하위 보고서|내용의 각 인스턴스에 대해 부모 항목이 반복됩니다.|  
|차트|각 차트 값에 대한 행과 멤버 레이블을 만들어 렌더링합니다. 계층 구조에서 계열 및 범주의 레이블은 결합되어 차트 값에 대한 행에 포함됩니다.|  
|데이터 막대|차트와 같이 렌더링하며 대개 계층이나 레이블을 포함하지 않습니다.|  
|스파크라인|차트와 같이 렌더링하며 대개 스파크라인은 계층이나 레이블을 포함하지 않습니다.|  
|계기|선형 눈금의 최소값과 최대값, 범위의 시작 값과 끝 값, 포인터의 값을 사용하여 한 레코드로 렌더링합니다.|  
|표시기|활성 상태 이름, 사용 가능한 상태 및 데이터 값을 포함하는 단일 레코드로 렌더링합니다.|  
|지도|지도 계층의 각 지도 멤버에 대한 레이블과 값을 사용하여 행을 렌더링합니다.<br /><br /> 지도에 여러 계층이 있는 경우 행의 값은 지도 계층에서 사용하는 지도 데이터 영역이 동일한지 여부에 따라 달라집니다. 여러 지도 계층에서 동일한 데이터 영역을 사용하는 경우 행에는 모든 계층의 데이터가 포함됩니다.|  
  
### <a name="hierarchical-and-grouped-data"></a>계층적 데이터 및 그룹화된 데이터  
 계층적 데이터와 그룹화된 데이터를 CSV 형식으로 표현하려면 결합해야 합니다.  
  
 렌더링 확장 프로그램은 보고서를 데이터 영역 내부의 중첩된 그룹을 표현하는 트리 구조로 결합합니다. 보고서는 다음과 같이 결합됩니다.  
  
-   행 계층 구조가 열 계층 구조보다 먼저 결합됩니다.  
  
-   열은 본문의 입력란이 왼쪽에서 오른쪽, 위쪽에서 아래쪽으로 정렬되고 그 다음에 데이터 영역이 왼쪽에서 오른쪽, 위쪽에서 아래쪽으로 정렬되는 방식으로 정렬됩니다.  
  
-   데이터 영역 내에서 열은 모퉁이 멤버, 행 계층 구조 멤버, 열 계층 구조 멤버, 셀 순으로 정렬됩니다.  
  
-   피어 데이터 영역은 공통 데이터 영역 또는 동적 상위 항목을 공유하는 데이터 영역 또는 동적 그룹입니다. 피어 데이터는 결합된 트리의 분기에 의해 식별됩니다.  
  
 자세한 내용은 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)MIME 형식을 반환합니다.  
  
  
##  <a name="RenderingModes"></a> 렌더러 모드  
 CSV 렌더링 확장 프로그램은 두 가지 모드로 작동할 수 있습니다. 하나는 Excel에 대해 최적화된 모드이고, 다른 하나는 RFC 4180에 지정된 CSV 사양의 엄격한 준수를 요구하는 타사 응용 프로그램에 최적화되어 있습니다. 사용하는 모드에 따라 피어 데이터 영역은 다르게 처리됩니다.  
  
### <a name="default-mode"></a>기본 모드  
 기본 모드는 Excel용으로 최적화되어 있습니다. 기본 모드로 렌더링되는 경우 보고서는 여러 섹션의 CSV로 렌더링된 데이터가 있는 CSV 파일로 렌더링됩니다. 각 피어 데이터 영역은 빈 줄에 의해 구분됩니다. 보고서 본문 내부의 피어 데이터 영역은 CSV 파일 내의 별도 데이터 블록으로 렌더링됩니다. 그 결과 다음과 같은 CSV 파일이 렌더링됩니다.  
  
-   보고서 본문의 개별 입력란은 CSV 파일 내부의 첫 번째 데이터 블록으로 한 번 렌더링됩니다.  
  
-   보고서 본문의 각 최상위 피어 데이터 영역은 자체 데이터 블록 안에 렌더링됩니다.  
  
-   중첩된 데이터 영역은 동일한 데이터 블록에 대각선 방향으로 렌더링됩니다.  
  
#### <a name="formatting"></a>서식  
 숫자 값은 지정된 서식 상태로 렌더링됩니다. Excel은 통화, 백분율, 날짜 등 서식이 지정된 숫자 값을 인식하여 CSV 파일을 가져올 때 각 셀에 적절하게 서식을 지정합니다.  
  
### <a name="compliant-mode"></a>규격 모드  
 규격 모드는 타사 응용 프로그램에 사용할 수 있도록 최적화되어 있습니다.  
  
#### <a name="data-regions"></a>데이터 영역  
 파일의 첫 번째 행에만 열 머리글이 들어 있으며 각 행에는 동일한 개수의 열이 있습니다.  
  
#### <a name="formatting"></a>서식  
 값에는 서식이 지정되지 않습니다.  
  
##  <a name="Interactivity"></a> 상호 작용  
 상호 작용은 이 렌더러에 의해 생성되는 어떤 CSV 형식에서도 지원되지 않습니다. 다음 대화형 요소는 렌더링되지 않습니다.  
  
-   하이퍼링크  
  
-   표시 또는 숨기기  
  
-   문서 구조  
  
-   드릴스루 또는 클릭 광고 링크  
  
-   최종 사용자 정렬  
  
-   고정 머리글  
  
-   책갈피  
  
  
##  <a name="DeviceInfo"></a> 장치 정보 설정  
 장치 정보 설정을 변경하여 렌더링할 모드, 구분 기호로 사용할 문자, 텍스트 한정자 기본 문자열로 사용할 문자 등 이 렌더러의 일부 기본 설정을 변경할 수 있습니다. 자세한 내용은 [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md)을 참조하세요.  
  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting services&#40;의 페이지 매김 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램 &#40;에 대 한 대화형 기능 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
