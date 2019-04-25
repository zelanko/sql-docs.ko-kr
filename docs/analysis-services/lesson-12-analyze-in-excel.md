---
title: '12 단원: Excel에서 분석 | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c42a45ec20edbde61a2f1b7c5b026f3467cd2371
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468443"
---
# <a name="lesson-12-analyze-in-excel"></a>12 단원: 도구 모음
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 SSDT에서 Excel 기능 분석을 사용 하 여 Microsoft Excel을 열고 모델 작업 영역으로 데이터 원본 연결을 자동으로 만드는 자동으로 워크시트에 피벗 테이블을 추가 합니다. Excel에서 분석 기능을 사용하면 모델을 배포하기 전에 모델 디자인의 효율성을 빠르고 손쉽게 테스트해 볼 수 있습니다. 이 단원에서는 데이터 분석을 수행하지 않습니다. 이 단원의 목표는 모델 작성자가 모델 디자인을 테스트하는 데 사용할 수 있는 도구를 익히도록 하는 것입니다. 분석을 사용 하 여 모델 작성자를 위한 Excel 기능에서 달리 최종 사용자에 게 배포 된 모델 데이터를 Excel 또는 Power BI에 연결 하 고 찾아보기와 같은 응용 프로그램을 보고 하는 클라이언트를 사용 합니다.  
  
이 단원을 완료 하려면 SSDT와 동일한 컴퓨터에 Excel이 설치 되어 있어야 합니다. 자세한 내용은 [Excel에서 분석](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)가 설치되어 있는 컴퓨터에 Excel이 설치되어 있어야 합니다.  
  
예상이 단원을 완료 시간: **20 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [11 단원: 역할을 만들](../analysis-services/lesson-11-create-roles.md)합니다.  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>기본 큐브 뷰 및 Internet Sales 큐브 뷰를 사용하여 검색  
이 첫 번째 태스크에서는 찾아보기는 모두 기본 큐브는 모든 모델 개체를 사용 하 여 및 인터넷 판매 큐브 뷰를 사용 하 여 모델에 앞서 있습니다. Internet Sales 큐브 뷰에는 Customer 테이블 개체가 제외되어 있습니다.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>기본 큐브 뷰를 사용하여 찾아보려면  
  
1.  클릭 합니다 **모델** 메뉴 > **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **확인**을 클릭합니다.  
  
    새 통합 문서와 함께 Excel이 열립니다. 현재 사용자 계정을 사용하여 데이터 원본이 연결되고 보기 가능한 필드를 정의하는 데 기본 큐브 뷰가 사용됩니다. 피벗 테이블은 워크시트에 자동으로 추가 됩니다.  
  
3.  Excel에서에 **피벗 테이블 필드 목록**, 확인 합니다 **DimDate** 및 **FactInternetSales** 측정값 그룹이 나타납니다 뿐만 **DimCustomer**, **DimDate**합니다 **DimGeography**를 **DimProduct**를 **DimProductCategory**,  **DimProductSubcategory**, 및 **FactInternetSales** 테이블이 모든 해당 열을 사용 하 여 표시 합니다.  
  
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 사용하여 찾아보려면  
  
1.  클릭 합니다 **모델** 메뉴를 클릭 한 다음 **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **현재 Windows 사용자**가 선택된 채로 두고 **큐브 뷰** 드롭다운 목록 상자에서 **Internet Sales**를 선택한 다음 **확인**을 클릭합니다. 
    
    ![as-tabular-lesson12-perspective](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  Excel에서의 **피벗 테이블 필드**, 확인 DimCustomer 테이블 필드 목록에서 제외 됩니다.  
    
    ![as-tabular-lesson12-fields](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## <a name="browse-by-using-roles"></a>역할을 사용 하 여 찾아보기  
역할은 테이블 형식 모델의 필수적인 부분입니다. 사용자가 멤버로 추가 되는 하나 이상의 역할이 없는 사용자 됩니다 액세스 하 고 모델을 사용 하 여 데이터를 분석할 수 있습니다. Excel에서 분석 기능은 정의한 역할을 테스트하는 방법을 제공합니다.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Sales Manager 사용자 역할을 사용 하 여 찾아보려면  
  
1.  SSDT에서 클릭 합니다 **모델** 메뉴를 클릭 한 다음 **Excel에서 분석**합니다.  
  
2.  에 **Excel에서 분석** 대화 상자의 **사용자 이름 또는 모델에 연결 하는 데 사용할 역할을 지정**를 선택 **역할**를 선택한 후 드롭다운 목록 상자에서 **판매 관리자**를 클릭 하 고 **확인**합니다.  
  
    새 통합 문서와 함께 Excel이 열립니다. 피벗 테이블을 자동으로 만들어집니다. 피벗 테이블 필드 목록에는 새 모델에서 사용할 수 있는 모든 데이터 필드가 포함되어 있습니다.  
      
3.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## <a name="whats-next"></a>다음 단계
다음 단원으로 이동 합니다. [단원 13: 배포](../analysis-services/lesson-13-deploy.md)합니다.

  
  
  
