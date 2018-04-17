---
title: 'Analysis Services tutorial 12 단원: Excel에서 분석 | Microsoft Docs'
description: Analysis Services tutorial 프로젝트에서 Excel에서 분석을 사용 하는 방법에 설명 합니다.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 17fee33ed671ba60625a2df7629890c8abbbaed5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="analyze-in-excel"></a>Excel에서 분석

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는를 Microsoft Excel을 열고 모델 작업 영역에 대 한 연결을 자동으로 만들기, 워크시트에 피벗 테이블을 자동으로 추가 기능 Excel에서에서 분석을 사용 합니다. Excel에서 분석 기능을 사용하면 모델을 배포하기 전에 모델 디자인의 효율성을 빠르고 손쉽게 테스트해 볼 수 있습니다. 이 단원에 있는 데이터 분석을 수행 하지 않습니다. 이 단원의 목표는 모델 작성자가 모델 디자인을 테스트하는 데 사용할 수 있는 도구를 익히도록 하는 것입니다.   
  
이 단원을 완료 하려면 Visual Studio와 같은 컴퓨터에 Excel이 설치 되어 있어야 합니다.
  
이 단원에 소요되는 예상 시간: **5분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [11 단원: 역할 만들기](../tutorial-tabular-1400/as-lesson-11-create-roles.md)합니다.  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>기본 큐브 뷰 및 Internet Sales 큐브 뷰를 사용하여 검색  

이러한 첫 번째 작업에서 모델을 찾으면 사용자 기본 큐브, 모든 모델 개체를 포함 하는 사용 하 여 및 인터넷 판매 큐브 뷰를 사용 하 여 앞서 있습니다. Internet Sales 큐브 뷰에는 Customer 테이블 개체가 제외되어 있습니다.  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>기본 큐브 뷰를 사용하여 찾아보려면  
  
1.  클릭는 **모델** 메뉴 > **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **확인**을 클릭합니다.  
  
    새 통합 문서와 Excel이 열립니다. 현재 사용자 계정을 사용하여 데이터 원본이 연결되고 보기 가능한 필드를 정의하는 데 기본 큐브 뷰가 사용됩니다. 피벗 테이블은 자동으로 워크시트에 추가 됩니다.  
  
3.  Excel에서의 **피벗 테이블 필드 목록**, 확인는 **DimDate** 및 **FactInternetSales** 측정값 그룹에 표시 합니다. **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales** 해당 열이 있는 테이블도 나타납니다.  
  
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>Internet Sales 큐브 뷰를 사용하여 찾아보려면  
  
1.  클릭는 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자에서 **현재 Windows 사용자** 가 선택된 채로 두고 **큐브 뷰** 드롭다운 목록 상자에서 **Internet Sales**를 선택한 다음 **확인**을 클릭합니다. 
    
    ![as-lesson12-perspective](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  Excel에서의 **피벗 테이블 필드**, DimCustomer 테이블은 필드 목록에서 제외를 확인 합니다.  
    
    ![as-lesson12-fields](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## <a name="browse-by-using-roles"></a>역할을 사용 하 여 찾아보기  

역할은 테이블 형식 모델의 중요 한 부분입니다. 사용자가 구성원으로 추가할 하나 이상의 역할이 없는 사용자가 액세스 하 고 모델을 사용 하 여 데이터를 분석할 수 없습니다. Excel에서 분석 기능은 정의한 역할을 테스트하는 방법을 제공합니다.  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>Sales Manager 사용자 역할을 사용 하 여 찾아보려면  
  
1.  SSDT에서는 클릭는 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.  
  
2.  **사용자 이름 또는 모델에 연결 하는 데 사용할 역할을 지정**선택, **역할**, 선택한 다음 드롭다운 목록 상자에서 **판매 관리자**, 클릭 하 고 **확인**합니다.  
  
    새 통합 문서와 Excel이 열립니다. 피벗 테이블을 자동으로 만들어집니다. 피벗 테이블 필드 목록에 새 모델에서 사용할 수 있는 모든 데이터 필드가 포함 되어 있습니다.  
      
3.  통합 문서를 저장하지 않은 채 Excel을 닫습니다.  
  
## <a name="whats-next"></a>다음 단계

다음 단원으로 이동: [13 단원: 배포](../tutorial-tabular-1400/as-lesson-13-deploy.md)합니다.

  
  
  
