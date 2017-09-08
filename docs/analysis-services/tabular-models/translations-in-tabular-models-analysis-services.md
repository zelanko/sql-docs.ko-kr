---
title: "테이블 형식 모델 (Analysis Services)에서 번역 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e67f88f5-9f0c-4f19-ab09-558c56ca9335
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 28ff4ea7472597ae86b426ec0a15de399f56d14f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="translations-in-tabular-models-analysis-services"></a>테이블 형식 모델 번역(Analysis Services )
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]테이블 형식 모델에 문자열 번역 지원을 추가합니다. 모델 내의 단일 개체는 이름 또는 설명이 여러 개로 번역되어 모델 정의 내에서 다중 언어 버전을 지원할 수 있습니다.  
  
 번역된 문자열은 Excel PivotTable 목록과 같이 클라이언트 도구에 표시되는 개체 메타데이터용(테이블 및 열의 이름 및 설명)으로만 사용됩니다.  번역된 문자열을 사용하려면 클라이언트 연결에 문화권을 지정합니다. **Excel에서 분석** 기능의 드롭다운 목록에서 언어를 선택할 수 있습니다. 다른 도구의 경우 연결 문자열에서 문화권을 지정해야 할 수 있습니다.  
  
 이 기능은 번역된 데이터를 모델로 로드하기 위한 용도가 아닙니다. 번역된 데이터 값을 로드하려면 해당 값을 제공하는 데이터 원본에서 번역된 문자열을 추출하는 처리 전략을 개발해야 합니다.  
  
 번역된 메타데이터를 추가하는 일반적인 워크플로는 다음과 같습니다.  
  
-   각 문자열을 번역하기 위한 자리 표시자가 포함된 비어 있는 번역 JSON 파일 생성  
  
-   JSON 파일에 문자열 번역 추가  
  
-   모델에 번역 다시 가져오기  
  
-   모델 빌드, 처리 또는 배포  
  
-   연결 문자열에서 LCID를 허용하는 클라이언트 응용 프로그램을 사용하는 모델 연결  
  
## <a name="create-an-empty-translation-file"></a>빈 번역 파일 만들기  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 을(를) 사용하여 번역을 추가합니다.  
  
1.  **모델** > **번역** > **번역 관리**를 클릭합니다.  
  
2.  번역을 제공할 언어를 선택한 후 **추가**를 클릭합니다.  
  
3.  나중에 문자열을 가져올 방법에 따라 목록에서 언어를 하나 이상 선택합니다.  
  
     번역 파일에는 다중 언어가 포함될 수 있지만 언어 당 번역 파일을 1개 생성하면 번역을 쉽게 관리할 수 있습니다. 생성 중인 번역 파일은 나중에 한 번에 가져옵니다. 언어별로 가져오기 옵션을 변경하려면 각 언어에 자체 파일이 있어야 합니다.  
  
4.  **언어 파일 내보내기**를 클릭합니다.  파일 이름과 설명을 입력합니다.  
  
 ![ssas 테이블 형식-변환-내보내기](../../analysis-services/tabular-models/media/ssas-tabular-translate-export.png "ssas 테이블 형식-변환-내보내기")  
  
## <a name="add-translations"></a>번역 추가  
 빈 JSON 번역 파일에는 특정 언어 번역에 대한 메타데이터가 포함됩니다. 개체 이름 및 설명에 대한 번역 자리 표시자는 모델 정의의 마지막에 있는 **Culture** 섹션에서 설명됩니다. 번역은 다음에 대하여 추가될 수 있습니다.  
  
|||  
|-|-|  
|translatedCaption|테이블 형식 모델의 모든 클라이언트 응용 프로그램 지원 시각화에 표시되는 테이블 또는 열 제목입니다.|  
|translatedDescription|캡션 보다는 덜 일반적인 설명은 SSDT 등의 모델링 도구의 모델 정보에 표시됩니다.|  
  
 파일에서 지정되지 않은 모든 메타데이터를 삭제하지 마십시오.  기반이 되는 파일와 일치해야 합니다. 원하는 문자열을 추가한 후 파일을 저장합니다.  
  
 수정이 필요해 보이지만  **referenceCulture** 섹션에는 모델의 기본 문화권에 메타데이터가 포함됩니다. **referenceCulture** 섹션에 적용된 모든 변경 내용은 가져오는 동안 읽지 않고 무시됩니다.  
  
 다음 예제에서는 **DimProduct** 및 **DimCustomer** 테이블에 대한 번역된 캡션 및 설명을 보여줍니다.  
  
 ![ssas-테이블 형식-변환-json](../../analysis-services/tabular-models/media/ssas-tabular-translate-json.png "ssas-테이블 형식-변환-json")  
  
> [!TIP]  
>  JSON 편집기를 사용하면 파일을 열 수 있지만 Visual Studio에서 JSON 편집기를 사용하여 솔루션 탐색기에서도 View Code 명령을 사용하여 SSDT에서 테이블 형식 모델 정의를 보는 것이 좋습니다. JSON 편집기를 다운로드하려면 [전체 Visual Studio 2015 버전이 설치](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)되어야 합니다. 무료 Community Edition에는 JSON 편집기 기능이 포함됩니다.  
  
## <a name="import-a-translation-file"></a>번역 파일 가져오기  
 가져온 번역 문자열은 모델 정의의 영구 부분이 됩니다. 문자열을 가져오면 번역 파일은 더 이상 참조되지 않습니다.  
  
1.  **모델** > **번역** > **번역 가져오기**를 클릭합니다.  
  
2.  변환 파일을 찾은 다음 **열기**를 클릭합니다.  
  
3.  선택 사항으로 가져오기 옵션을 지정합니다.  
  
    |||  
    |-|-|  
    |기존 번역 덮어쓰기|동일 언어의 모든 기존 캡션 또는 설명을 가져올 파일로 대체합니다.|  
    |잘못된 개체 무시|메타 데이터 불일치를 무시하거나 오류로 표시할지의 여부를 지정합니다.|  
    |로그 파일에 가져오기 결과 쓰기|로그 파일은 기본적으로 프로젝트 폴더에 저장됩니다. 가져오기를 완료한 후에 정확한 파일 경로를 입력합니다. 로그 파일 이름이 SSDT_Translations_Log_\<타임 스탬프 > 합니다.|  
    |JSON 파일에 번역 백업 후 가져오기|가져올 문자열의 문화권과 일치하는 기존 번역을 백업합니다.  모델에 가져올 문화권이 없는 경우 백업은 비어있게 됩니다.<br /><br /> 나중이 이 파일을 복구해야 하는 경우 model.bim의 내용을 이 JSON 파일로 교체할 수 있습니다.|  
  
4.  **가져오기**를 클릭합니다.  
  
5.  필요에 따라 로그 파일 또는 백업을 생성한 경우 이 파일을 프로젝트 폴더(예: C:\Users\Documents\Visual Studio 2015\Projects\Tabular1200-AW\Tabular1200-AW)에서 찾을 수 있습니다.  
  
6.  가져오기를 확인하려면 다음 단계를 수행:  
  
    -   솔루션 탐색기에서 **model.bim** 파일을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택합니다. **예** 를 클릭해서 디자인 뷰를 종료하고 코드 보기에서 **model.bim** 을 다시 엽니다.  무료 Community Edition 등 Visual Studio의 전체 버전을 설치한 경우 파일은 기본 JSON 편집기에서 열립니다.  
  
    -   **문화권** 또는 번역된 특정 문자열을 검색하여 원하는 문자열이 해당 위치에 실제로 있는지 확인합니다.  
  
## <a name="connect-using-a-locale-identifier"></a>로캘 ID를 사용하여 연결  
 이 섹션에는 모델에서 올바른 문자열이 반환되는지를 확인하는 방법을 설명합니다.  
  
1.  Excel에서 테이블 형식 모델에 연결합니다. 이 단계에서는 모델이 배포된 것으로 가정합니다. 모델이 작업 영역에만 있는 경우 Analysis Services 인스턴스에 배포하여 유효성 검사를 완료합니다.  
  
     아니면, **Excel에서 분석** 기능을 사용하여 모델에 연결합니다.  
  
2.  Excel 연결 대화 상자에서 문자열 번역이 모델에 존재하는 문화권을 선택합니다. Excel은 모델에 정의된 문화권을 감지하고 그에 따라 드롭다운 목록을 채웁니다.  
  
     ![ssas-테이블 형식-번역-excel](../../analysis-services/tabular-models/media/ssas-tabular-translations-excel.png "ssas-테이블 형식-번역-excel")  
  
     피벗 테이블을 만드는 경우 번역된 테이블 및 열 이름을 확인해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services의 세계화 시나리오](../../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
