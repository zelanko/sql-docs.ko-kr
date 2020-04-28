---
title: 도구 모음 (브라우저 탭, 큐브 디자이너) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a1c6272d-e514-456b-9995-b73fec0112a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d1135be55065ab62e649d84c00cec4eebf60b58
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175582"
---
# <a name="toolbar-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>도구 모음(브라우저 탭, 큐브 디자이너)(Analysis Services - 다차원 데이터)
  큐브 디자이너의 **도구 모음** 에 있는 기능을 사용하여 큐브 또는 해당 개체를 디자인하거나 찾아보는 동안, 또는 MDX 쿼리를 만드는 동안 일반적인 작업을 수행할 수 있습니다. 디자인 타임과 쿼리 뷰에 공통적인 작업에는 사용자 컨텍스트 설정, 개체 처리 및 기본 언어 설정 등이 있습니다.

 다음 표에서는 **도구 모음** 단추와 해당 기능을 보여 줍니다.

|단추|설명|
|------------|-----------------|
|**텍스트로 편집**|이 데이터 원본 유형에 대해서는 사용할 수 없습니다.|
|**가져오기**|파일 시스템의 보고서 정의 파일(.rdl)에서 기존 쿼리를 가져옵니다.|
|![MDX 쿼리 뷰로 변경](media/rsqdicon-commandtypemdx.gif "MDX 쿼리 뷰로 변경")|MDX 명령 유형으로 전환합니다.|
|![결과 데이터 새로 고침](media/rsqdicon-refresh.gif "결과 데이터 새로 고침")|데이터 원본의 메타데이터를 새로 고칩니다.|
|![계산 멤버 추가](media/rsqdicon-addcalculatedmember.gif "계산 멤버 추가")|**계산 멤버 작성기** 대화 상자를 표시합니다.|
|![빈 셀 표시 설정/해제](media/rsqdicon-showemptycells.gif "빈 셀 표시 설정/해제")|데이터 창에서 빈 셀을 표시하거나 표시하지 않는 기능 사이를 전환합니다. 이것은 MDX에 NON EMPTY 절을 사용하는 것과 동일합니다.|
|![쿼리 자동 실행](media/rsqdicon-autoexecute.gif "쿼리 자동 실행")|변경이 수행될 때마다 쿼리를 자동으로 실행하고 결과를 표시합니다. 결과는 데이터 창에 표시됩니다.|
|![집계 표시 단추](media/rsqdicon-showaggregations.gif "집계 표시 단추")|데이터 창에서 집계를 표시합니다.|
|![Delete](media/rsqdicon-delete.gif "삭제")|데이터 창의 선택된 열을 쿼리에서 삭제합니다.|
|![쿼리 매개 변수 대화 상자 아이콘](media/iconqueryparameter.gif "쿼리 매개 변수 대화 상자 아이콘")|**쿼리 매개 변수** 대화 상자를 표시합니다. 쿼리 매개 변수의 값을 지정하면 같은 이름의 매개 변수가 자동으로 만들어집니다.|
|![쿼리 준비 단추](media/rsqdicon-preparequery.gif "쿼리 준비 단추")|쿼리를 준비합니다.|
|![쿼리 실행](media/rsqdicon-run.gif "쿼리 실행")|쿼리를 실행하고 데이터 창에 결과를 표시합니다.|
|![쿼리 취소](media/rsqdicon-cancel.gif "쿼리 취소")|쿼리를 취소합니다.|
|![디자인 모드로 전환](media/rsqdicon-designmode.gif "디자인 모드로 전환")|디자인 모드와 쿼리 모드 사이를 전환합니다.|

 일반적으로 **디자인 모드** 와 **쿼리 모드**의 도구 모음 단추는 같습니다. 하지만 쿼리 모드에서는 다음 단추를 사용할 수 없습니다.

-   **텍스트로 편집**

-   **계산 멤버 추가**(![계산 멤버 추가](media/rsqdicon-addcalculatedmember.gif "계산 멤버 추가"))

-   **빈 셀 표시**(![빈 셀 표시 설정/해제](media/rsqdicon-showemptycells.gif "빈 셀 표시 설정/해제"))

-   **자동 실행**(![쿼리 자동 실행](media/rsqdicon-autoexecute.gif "쿼리 자동 실행"))

-   **집계 표시**(![집계 표시 단추](media/rsqdicon-showaggregations.gif "집계 표시 단추"))

## <a name="options"></a>옵션

|옵션|설명|
|------------|-----------------|
|**프로세스**|**처리** 대화 상자를 표시하고 큐브를 처리하려면 클릭합니다. **처리** 대화 상자에 대한 자세한 내용은 [처리 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](process-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|
|**사용자 변경**|**보안 컨텍스트** 대화 상자를 표시 하 고 **브라우저** 탭에서 사용 되는 사용자 및 역할을 변경 하려면 클릭 합니다. **보안 컨텍스트** 대화 상자에 대 한 자세한 내용은 [Analysis Services 다차원 데이터&#41;&#40;보안 컨텍스트 대화 상자 ](security-context-dialog-box-analysis-services-multidimensional-data.md)를 참조 하세요.|
|**연결할**|**브라우저** 탭에 대한 세션의 연결이 연결 오류나 제한 시간 초과 등의 이유로 인해 끊긴 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 계산 **탭을 큐브가 포함된** 인스턴스 및 데이터베이스에 다시 연결하려면 클릭합니다.|
|**새로 고침**|**메타데이터** 및 **보고서** 창을 새로 고치려면 클릭합니다.|
|**오름차순 정렬**|**보고서** 창에서 선택한 행의 형제를 **언어**에서 지정한 언어에 대해 오름차순으로 정렬하려면 클릭합니다.<br /><br /> **참고** 이 옵션은 **보고서** 창에서 셀을 선택한 경우에만 사용할 수 있습니다.|
|**내림차순 정렬**|**보고서** 창에서 선택한 행의 형제를 **언어**에서 지정한 언어에 대해 내림차순으로 정렬하려면 클릭합니다.<br /><br /> 참고:이 옵션은 **보고서** 창에서 셀을 선택한 경우에만 사용할 수 있습니다.|
|**자동 필터**|**결과** 창에서 결과를 자동으로 필터링하려면 클릭합니다.|
|**최상위/최하위만 표시**|선택한 측정값을 기준으로 **보고서** 창에 있는 셀의 최상위 또는 최하위 숫자나 백분율만 표시하려면 값 또는 백분율을 선택합니다.<br /><br /> 이 옵션에 대한 자세한 내용은 [TopCount&#40;MDX&#41;](/sql/mdx/topcount-mdx), [TopPercent&#40;MDX&#41;](/sql/mdx/toppercent-mdx), [BottomCount&#40;MDX&#41;](/sql/mdx/bottomcount-mdx) 및 [BottomPercent&#40;MDX&#41;](/sql/mdx/bottompercent-mdx)를 참조하세요.|
|**소계**|부분합을 표시하려면 클릭합니다.|
|**모든 항목 합계**|**보고서** 창에 있는 모든 멤버의 합계를 표시하려면 클릭합니다.|
|**빈 셀 표시**|**보고서** 창의 빈 셀을 표시하려면 클릭합니다.|
|**결과 지우기**|**보고서** 창의 결과를 지우려면 클릭합니다.|
|**명령 및 옵션**|**명령 및 옵션** 대화 상자를 표시하고 **보고서** 창의 Microsoft Office 11.0 피벗 테이블 컨트롤에 대한 고급 속성을 편집하려면 클릭합니다. **명령 및 옵션** 대화 상자에 대한 자세한 내용은 Microsoft Office 설명서를 참조하십시오.|
|**관점**|**메타데이터** 및 **보고서** 창에서 데이터 및 메타데이터를 볼 큐브 뷰를 선택합니다.<br /><br /> 큐브 뷰를 사용하지 않고 큐브를 보려면 큐브 이름을 선택합니다.|
|**언어**|**메타데이터** 및 **보고서** 창에서 데이터 및 메타데이터를 볼 언어를 선택합니다.<br /><br /> 기본 언어를 사용하여 큐브를 보려면 **기본값**을 선택합니다.|


