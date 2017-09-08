---
title: "12 단원: 역할 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 659b8bb8af4d759367d81bb3e8828360fd2b1f28
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-11-create-roles"></a>11단원: 역할 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 역할을 만듭니다. 역할은 역할 멤버인 Windows 사용자로만 액세스를 제한함으로써 모델 데이터베이스 개체 및 데이터에 보안을 제공합니다. 각 역할은 없음, 읽기, 읽기 및 처리, 처리 또는 관리자라는 단일 사용 권한으로 정의됩니다. 역할 관리자를 사용 하 여 모델을 제작 하는 동안 역할을 정의할 수 있습니다. 모델을 배포한 후 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 역할을 관리할 수 있습니다. 자세한 내용은 [역할](../analysis-services/tabular-models/roles-ssas-tabular.md)의 역할 관리자 대화 상자를 사용하여 역할을 정의할 수 있습니다.  
  
> [!NOTE]  
> 이 자습서를 완료하기 위해 역할을 만들 필요는 없습니다. 기본적으로 현재 로그인하는 데 사용한 계정에는 모델에 대한 관리자 권한이 있습니다. 그러나 다른 사용자가 조직의 보고 클라이언트를 사용 하 여 모델을 찾아볼 수 있도록 사용 권한을 읽기 역할을 하나 이상 만들 하며 해당 사용자가 구성원으로 추가 합니다.  
  
다음과 같은 세 개의 역할을 만듭니다.  
  
-   **영업 관리자** –이 역할 모든 모델 개체와 데이터에 읽기 권한이 하려는 조직에서 사용자를 포함할 수 있습니다.  
  
-   **Sales Analyst US** –이 역할에 미국 내에서 판매와 관련 된 데이터를 탐색할 수에 할당할 조직의 사용자를 포함할 수 있습니다. 이 역할에 대해 DAX 수식을 사용하여 멤버가 미국에 대한 데이터만 검색할 수 있도록 제한하는 *행 필터*를 정의합니다.  
  
-   **관리자** –이 역할에서 관리자 권한을 할당 해 무제한 액세스 및 model 데이터베이스에서 관리 작업을 수행할 수 있는 권한이 있는 사용자를 포함할 수 있습니다.  
  
조직의 Windows 사용자 및 그룹 계정은 고유하므로 특정 조직의 계정을 멤버에 추가할 수 있습니다. 그러나 이 자습서에서는 멤버를 비워둘 수도 있습니다. 나중에 12단원: Excel에서 분석에서 각 역할의 영향을 테스트할 수 있습니다.  
  
이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [10 단원: 파티션 만들기](../analysis-services/lesson-10-create-partitions.md)합니다.  
  
## <a name="create-roles"></a>역할 만들기  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Sales Manager 사용자 역할을 만들려면  
  
1.  테이블 형식 모델 탐색기에서 마우스 오른쪽 단추로 클릭 **역할** > **역할**합니다.  
  
2.  역할 관리자에서 클릭 **새로**합니다.  
  
3.  새 역할을 선택한 다음 클릭은 **이름** 열을 역할 이름 바꾸기 **판매 관리자**합니다.  
  
4.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **읽기** 권한을 선택합니다. 

    ![으로 테이블 형식-lesson11-새-역할](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  선택 사항: 클릭는 **멤버** 탭을 클릭 한 다음 **추가**합니다. **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Sales Analyst US 사용자 역할을 만들려면  
  
1.  역할 관리자에서 클릭 **새로**합니다.    
  
2.  역할 이름 바꾸기 **Sales Analyst US**합니다.  
  
3.  이 역할을 부여 **읽기** 권한.  
  
4.  행 필터 탭 한 다음에 대 한 클릭는 **DimGeography** 테이블만 DAX 필터 열에 다음 수식을 입력 합니다.  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    행 필터 수식은 부울(TRUE/FALSE) 값으로 확인되어야 합니다. 이 수식을 사용하면 Country Region Code 값이 "US"인 행만 사용자에게 표시되도록 지정됩니다.  
    ![으로 테이블 형식-lesson11-역할-필터](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  옵션: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다. **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
#### <a name="to-create-an-administrator-user-role"></a>관리자 사용자 역할을 만들려면  
  
1.  **새로 만들기**를 클릭합니다.  
  
2.  역할 이름 바꾸기 **관리자**합니다.  
  
3.  이 역할을 부여 **관리자** 권한.  
  
4.  옵션: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다. **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다. 
  
  
## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [12 단원: Excel에서 분석](../analysis-services/lesson-12-analyze-in-excel.md)합니다.

  
  

