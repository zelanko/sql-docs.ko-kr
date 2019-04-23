---
title: 'Analysis Services 자습서 단원 12: Excel에서 분석 | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 4c1b433ae2023f544073e285cca9594c980dd83f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945379"
---
# <a name="analyze-in-excel"></a>도구 모음

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 Microsoft Excel을 열고 모델 작업 영역에 대 한 연결을 자동으로 만듭니다, 자동으로 워크시트에 피벗 테이블을 추가 하려면 Excel 기능에서 분석을 사용 합니다. Excel에서 분석 기능을 사용하면 모델을 배포하기 전에 모델 디자인의 효율성을 빠르고 손쉽게 테스트해 볼 수 있습니다. 이 단원에는 어떠한 데이터 분석도 수행 하지 않습니다. 이 단원의 목표는 모델 작성자가 모델 디자인을 테스트하는 데 사용할 수 있는 도구를 익히도록 하는 것입니다.   
  
이 단원을 완료 하려면 Visual Studio와 동일한 컴퓨터에 Excel이 설치 되어 있어야 합니다.
  
예상이 단원을 완료 시간: **5 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [11 단원: 역할을 만들](../tutorial-tabular-1400/as-lesson-11-create-roles.md)합니다.  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>기본 큐브 뷰 및 Internet Sales 큐브 뷰를 사용하여 검색  

이러한 첫 번째 작업을 모두 기본 큐브는 모든 모델 개체를 사용 하 여 모델을 찾아보고에 인터넷 판매 큐브 뷰를 사용 하 여 이전에 만든 합니다. Internet Sales 큐브 뷰에는 Customer 테이블 개체가 제외되어 있습니다.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>기본 큐브 뷰를 사용하여 찾아보려면  
  
1.  클릭 합니다 **모델** 메뉴 > **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **확인**을 클릭합니다.  
  
    Excel에서 새 통합 문서가 열립니다. 현재 사용자 계정을 사용하여 데이터 원본이 연결되고 보기 가능한 필드를 정의하는 데 기본 큐브 뷰가 사용됩니다. 피벗 테이블은 워크시트에 자동으로 추가 됩니다.  
  
3.  Excel에서에 **피벗 테이블 필드 목록**, 확인 합니다 **DimDate** 및 **FactInternetSales** 측정값 그룹이 나타납니다. 합니다 **DimCustomer**, **DimDate**를 **DimGeography**를 **DimProduct**를 **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales** 해당 열을 사용 하 여 테이블도 나타납니다.  
  
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 사용하여 찾아보려면  
  
1.  클릭 합니다 **모델** 메뉴를 클릭 한 다음 **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **현재 Windows 사용자**가 선택된 채로 두고 **큐브 뷰** 드롭다운 목록 상자에서 **Internet Sales**를 선택한 다음 **확인**을 클릭합니다. 
    
    ![as-lesson12-perspective](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  Excel에서의 **피벗 테이블 필드**, 확인 DimCustomer 테이블 필드 목록에서 제외 됩니다.  
    
    ![as-lesson12-fields](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## <a name="browse-by-using-roles"></a>역할을 사용 하 여 찾아보기  

역할은 테이블 형식 모델의 중요 한 부분입니다. 사용자가 멤버로 추가 되는 하나 이상의 역할이 없는 사용자가 액세스 하 고 모델을 사용 하 여 데이터를 분석할 수 없습니다. Excel에서 분석 기능은 정의한 역할을 테스트하는 방법을 제공합니다.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Sales Manager 사용자 역할을 사용 하 여 찾아보려면  
  
1.  SSDT에서 클릭 합니다 **모델** 메뉴를 클릭 한 다음 **Excel에서 분석**합니다.  
  
2.  **사용자 이름 또는 모델에 연결 하는 데 사용할 역할을 지정**를 선택 **역할**를 선택한 후 드롭다운 목록 상자에서 **Sales Manager**를 클릭및**확인**합니다.  
  
    Excel에서 새 통합 문서가 열립니다. 피벗 테이블을 자동으로 만들어집니다. 피벗 테이블 필드 목록에는 새 모델에서 사용할 수 있는 모든 데이터 필드가 포함 됩니다.  
      
3.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## <a name="whats-next"></a>다음 단계

다음 단원으로 이동 합니다. [단원 13: 배포](../tutorial-tabular-1400/as-lesson-13-deploy.md)합니다.

  
  
  
