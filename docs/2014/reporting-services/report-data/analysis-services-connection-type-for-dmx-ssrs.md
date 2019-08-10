---
title: DMX용 Analysis Services 연결 형식(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 851c26db9ce953315c9d01b77596c7cb1b92e8c4
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891025"
---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>DMX용 Analysis Services 연결 형식(SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본을 사용하여 데이터 세트를 만들면 올바른 큐브가 검색될 경우 보고서 디자이너에 MDX(Multidimensional Expressions) 쿼리 디자이너가 표시됩니다. 큐브가 검색되지 않지만 데이터 마이닝 모델을 사용할 수 있는 경우에는 보고서 디자이너에 DMX(Data Mining Extension) 쿼리 디자이너가 표시됩니다. MDX와 DMX 디자이너 사이를 전환하려면 도구 모음에서 **DMX 명령 유형**(![DMX 쿼리 언어 뷰로 변경](../media/rsqdicon-commandtypedmx.gif "DMX 쿼리 언어 뷰로 변경")) 단추를 클릭합니다. DMX 쿼리 디자이너에서는 그래픽 요소를 사용하여 DMX 쿼리를 대화형으로 작성할 수 있습니다. DMX 쿼리 디자이너를 사용하려면 지정한 데이터 원본에는 이미 데이터를 제공하는 데이터 마이닝 모델이 있어야 합니다. 쿼리 결과는 보고서에 사용되는 일반 행 집합으로 변환됩니다.  
  
> [!NOTE]  
>  보고서를 디자인하기 전에 모델을 학습해야 합니다. 자세한 내용은 [데이터 마이닝 솔루션](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)을 참조하세요.  
  
## <a name="design-mode"></a>디자인 모드  
 DMX 쿼리 디자이너는 디자인 모드에서 열립니다. 디자인 모드에는 단일 데이터 마이닝 모델과 입력 테이블을 선택하는 데 사용하는 그래픽 디자인 화면과 예측 쿼리를 지정하는 데 사용하는 표가 포함되어 있습니다. DMX 쿼리 디자이너에는 두 가지 다른 모드가 있습니다. 쿼리 모드와 결과 모드가 있습니다. 쿼리 모드에서는 디자인 모드의 표가 DMX 쿼리를 입력하는 데 사용할 수 있는 쿼리 창으로 바뀝니다. 결과 모드에서는 쿼리에서 반환된 결과 집합이 데이터 표에 나타납니다.  
  
 DMX 쿼리 디자이너의 모드를 변경하려면 쿼리 디자인 화면을 마우스 오른쪽 단추로 클릭하고 **디자인**, **쿼리**또는 **결과**를 선택합니다. 자세한 내용은 [Analysis Services DMX 쿼리 디자이너 사용자 인터페이스](analysis-services-dmx-query-designer-user-interface.md) 및 [데이터 마이닝 모델에서 데이터 검색&#40;DMX&#41;&#40;SSRS&#41;](retrieve-data-from-a-data-mining-model-dmx-ssrs.md)을 참조하세요.  
  
## <a name="designing-a-prediction-query"></a>예측 쿼리 디자인  
 디자인 모드의 쿼리 디자인 창에는 다음과 같은 두 개의 창이 있습니다. **마이닝 모델** 및 **입력 테이블을 선택**합니다. **마이닝 모델** 창을 사용하여 쿼리에 사용할 마이닝 모델을 선택하고 **입력 테이블 선택** 창을 사용하여 예측의 기반이 될 테이블을 선택할 수 있습니다. 입력 테이블 대신 단일 쿼리를 사용하려면 쿼리 디자인 창을 마우스 오른쪽 단추로 클릭하고 **단일 쿼리**를 선택합니다. **입력 테이블 선택** 창이 **단일 쿼리 입력** 창으로 바뀝니다.  
  
 디자인 모드에서 **마이닝 모델** 및 **입력 테이블 선택** 창의 필드를 표 형태 창의 **필드** 열로 끕니다. 나머지 열을 채워 별칭을 지정하고, 결과에 해당 필드를 표시하고, 여러 필드를 그룹화하고, 연산자를 지정하여 필드 값을 지정한 기준 또는 인수로 제한할 수도 있습니다. 쿼리 모드에 있는 경우 필드를 쿼리 창으로 끌어 DMX 쿼리를 작성합니다.  
  
## <a name="using-parameters"></a>매개 변수 사용  
 DMX 쿼리 매개 변수에 보고서 매개 변수를 전달할 수 있습니다. 이렇게 하려면 DMX 쿼리에 매개 변수를 추가하고 **쿼리 매개 변수** 대화 상자에서 쿼리 매개 변수를 정의한 다음 관련 보고서 매개 변수를 수정해야 합니다. 쿼리 매개 변수를 정의하려면 도구 모음에서 **쿼리 매개 변수**(![쿼리 매개 변수 대화 상자의 아이콘](https://docs.microsoft.com/analysis-services/analysis-services/media/iconqueryparameter.gif "쿼리 매개 변수 대화 상자의 아이콘")) 단추를 클릭합니다. DMX 쿼리의 매개 변수를 정의하는 방법에 대한 지침을 보려면 [Analysis Services용 MDX 쿼리 디자이너에서 매개 변수 정의&#40;보고서 작성기 및 SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md)를 참조하세요.  
  
 보고서 매개 변수와 쿼리 매개 변수 간의 관계를 관리하는 방법에 대한 자세한 내용은 [보고서 매개 변수와 쿼리 매개 변수 연결&#40;보고서 작성기 및 SSRS&#41;](associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)을 참조하세요. 매개 변수에 대한 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 솔루션](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)   
 [보고서 디자이너 SQL Server Data Tools &#40;SSRS의 쿼리 디자인 도구&#41;](query-design-tools-ssrs.md)   
 [보고서 서비스의 데이터 연결, 데이터 원본 및 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
