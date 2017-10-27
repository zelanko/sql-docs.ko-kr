---
title: "Analysis Services 용 MDX 쿼리 디자이너에서 매개 변수 정의 | Microsoft Docs"
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
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f989ec80fe80d85381673cb12a90b8e3cea82da4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services"></a>Analysis Services용 MDX 쿼리 디자이너에서 매개 변수 정의
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에 대한 MDX 쿼리를 매개 변수화하려면 쿼리 매개 변수를 쿼리에 추가해야 합니다. MDX 쿼리 디자이너에서 필터를 지정하여 디자인 모드와 쿼리 모드 모두에서 쿼리 매개 변수를 추가할 수 있습니다. 쿼리 매개 변수를 사용하여 쿼리를 정의하면 Reporting Services에서 자동으로 보고서 매개 변수 및 데이터 집합을 만들어 올바른 값 목록을 제공합니다. 따라서 사용자는 쿼리에 직접 전달되는 값을 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>디자인 모드에서 MDX의 쿼리 매개 변수를 정의하려면  
  
1.  보고서 데이터 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본 유형에서 만든 데이터 집합을 마우스 오른쪽 단추로 클릭한 다음 **쿼리**를 클릭합니다. MDX 쿼리 디자이너가 디자인 모드에서 열립니다.  
  
2.  차원을 필터 영역으로 끈 다음 **차원** 열의 첫 번째 셀 위에 놓습니다.  
  
3.  **계층** 열의 드롭다운 목록에서 값을 선택합니다.  
  
4.  **연산자** 열의 드롭다운 목록에서 연산자를 선택합니다.  
  
5.  **필터 식** 열의 드롭다운 목록에서 개별 값을 선택하거나 **모든** 멤버를 클릭하여 모든 값을 선택합니다.  
  
6.  **매개 변수** 열에서 확인란을 선택하여 보고서 매개 변수를 만듭니다.  
  
7.  **실행**을 클릭합니다.  
  
     쿼리를 실행한 후 도구 모음의 **디자인** 을 클릭하여 쿼리 모드로 전환한 다음 작성된 MDX 쿼리를 봅니다. 계속 디자인 모드를 사용하여 쿼리를 개발하려는 경우 쿼리 모드에서 쿼리 텍스트를 변경하지 마십시오. **디자인** 을 클릭하여 디자인 모드로 다시 전환합니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     보고서 데이터 창에서 매개 변수 노드를 확장하여 필터에 대해 자동으로 만든 보고서 매개 변수를 표시합니다.  
  
     보고서 매개 변수에 대해 사용 가능한 값을 제공하는 데이터 집합을 보려면 보고서 데이터 창의 빈 영역을 마우스 오른쪽 단추로 클릭한 다음 **숨겨진 데이터 집합 표시**를 클릭합니다. 보고서 데이터 창에 보고서의 모든 데이터 집합이 표시됩니다.  
  
### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>쿼리 모드에서 MDX의 쿼리 매개 변수를 정의하려면  
  
1.  보고서 데이터 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본 유형에서 만든 데이터 집합을 마우스 오른쪽 단추로 클릭한 다음 **쿼리**를 클릭합니다. MDX 쿼리 디자이너가 디자인 모드에서 열립니다.  
  
2.  도구 모음에서 **디자인** 을 클릭하여 쿼리 모드로 전환합니다.  
  
3.  MDX 쿼리 디자이너 도구 모음을 클릭 하 여 **쿼리 매개 변수** (![쿼리 매개 변수 대화 상자에 대 한 아이콘](../../reporting-services/report-data/media/iconqueryparameter.gif "쿼리 매개 변수 대화 상자에 대 한 아이콘")). 쿼리 매개 변수 대화 상자가 열립니다.  
  
4.  에 **매개 변수** 열을 클릭 하 여  **\<매개 변수 입력 >**, 한 다음 매개 변수 이름을 입력 합니다.  
  
5.  **차원** 열의 드롭다운 목록에서 값을 선택합니다.  
  
6.  **계층** 열의 드롭다운 목록에서 값을 선택합니다.  
  
7.  **다중 값** 열에서 확인란을 선택하여 다중 값 매개 변수를 만듭니다.  
  
8.  5단계에서 선택한 사항에 따라 **기본값** 열의 드롭다운 목록에서 단일 값 또는 다중 값을 선택합니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 쿼리 디자이너 도구 모음에서 **실행**을 클릭합니다.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     보고서 데이터 창에서 매개 변수 노드를 확장하여 필터에 대해 자동으로 만든 보고서 매개 변수를 표시합니다.  
  
     보고서 매개 변수에 대해 사용 가능한 값을 제공하는 데이터 집합을 보려면 보고서 데이터 창의 빈 영역을 마우스 오른쪽 단추로 클릭한 다음 **숨겨진 데이터 집합 표시**를 클릭합니다. 보고서 데이터 창에 보고서의 모든 데이터 집합이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [MDX &#40; analysis Services 연결 유형 Ssrs&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)   
 [Analysis Services MDX 쿼리 디자이너 사용자 인터페이스](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
  

