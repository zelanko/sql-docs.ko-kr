---
title: 'Analysis Services 자습서 단원 11: 역할 만들기 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
ms.openlocfilehash: 8e630d53aed8f722c2de4a21afea8391cefe8bd8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981075"
---
# <a name="create-roles"></a>역할 만들기

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 단원에서는 역할을 만듭니다. 역할은 역할 멤버인 사용자 에게만 액세스를 제한 하 여 모델 데이터베이스 개체 및 데이터 보안을 제공 합니다. 각 역할은 없음, 읽기, 읽기 및 처리, 처리 또는 관리자라는 단일 사용 권한으로 정의됩니다. 역할 관리자를 사용 하 여 모델을 제작 하는 동안 역할을 정의할 수 있습니다. 모델을 배포한 후에 SQL Server Management Studio (SSMS)를 사용 하 여 역할을 관리할 수 있습니다. 자세한 내용은 참조 하세요 [역할](../tabular-models/roles-ssas-tabular.md)입니다.
  
> [!NOTE]  
> 이 자습서를 완료하기 위해 역할을 만들 필요는 없습니다. 기본적으로에 현재 로그온 계정에 관리자 권한 모델. 그러나 보고 클라이언트를 사용 하 여 찾아보려면 조직의 다른 사용자에 대 한 사용 권한을 읽기를 사용 하 여 하나 이상의 역할을 만들 하며 해당 사용자를 멤버로 추가 합니다.  
  
세 가지 역할을 만들 있습니다.  
  
-   **영업 관리자** –이 역할 모든 모델 개체 및 데이터에 읽기 권한이 하려는 조직에서 사용자를 포함할 수 있습니다.  
  
-   **Sales Analyst US** –이 역할 미국 내에서 판매와 관련 된 데이터를 찾아볼 수에 원하는 조직에서 사용자를 포함할 수 있습니다. 이 역할에 대해 정의 하는 DAX 수식을 사용을 *행 필터*, 미국에만 데이터를 이동할 멤버를 제한 합니다.  
  
-   **관리자** –이 역할에서 무제한 액세스 및 권한을 model 데이터베이스에서 관리 작업을 수행할 수 있는 관리자 권한을 할당 하려는 사용자를 포함할 수 있습니다.  
  
조직의 Windows 사용자 및 그룹 계정은 고유하므로 특정 조직의 계정을 멤버에 추가할 수 있습니다. 그러나 이 자습서에서는 멤버를 비워둘 수도 있습니다. 나중에 12 단원 각 역할의 효과 테스트 합니다: Excel에서 분석 합니다.  
  
이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [단원 10: 파티션 만들기](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)합니다.  
  
## <a name="create-roles"></a>역할 만들기  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Sales Manager 사용자 역할을 만들려면  
  
1.  테이블 형식 모델 탐색기에서 마우스 오른쪽 단추로 클릭 **역할** > **역할**입니다.  
  
2.  역할 관리자에서 클릭 **새로 만들기**합니다.  
  
3.  새 역할을 클릭 한 다음 합니다 **이름** 열을 역할 이름 바꾸기 **Sales Manager**합니다.  
  
4.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **읽기** 권한을 선택합니다. 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  선택 사항: 클릭 합니다 **멤버** 탭을 클릭 한 다음 **추가**합니다. **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Sales Analyst US 사용자 역할을 만들려면  
  
1.  역할 관리자에서 클릭 **새로 만들기**합니다.    
  
2.  역할 이름 바꾸기 **Sales Analyst US**합니다.  
  
3.  이 역할을 부여 **읽기** 권한.  
  
4.  행 필터 탭을 클릭 한 후 합니다 **DimGeography** 테이블만 DAX 필터 열에 다음 수식을 입력 합니다.  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    행 필터 수식은 부울(TRUE/FALSE) 값으로 확인되어야 합니다. 이 수식을 사용 하 여 Country Region Code 값을 가진 행만 "us" 사용자에 게 표시 되는지 지정 합니다.  
    ![as-lesson11-role-filter](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  선택 사항: 클릭 합니다 **멤버** 탭을 클릭 한 다음 **추가**합니다. **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
#### <a name="to-create-an-administrator-user-role"></a>관리자 사용자 역할을 만들려면  
  
1.  **새로 만들기**를 클릭합니다.  
  
2.  역할 이름 바꾸기 **관리자**합니다.  
  
3.  이 역할을 부여 **관리자** 권한.  
  
4.  선택 사항: 클릭 합니다 **멤버** 탭을 클릭 한 다음 **추가**합니다. **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다. 
  
  
## <a name="whats-next"></a>다음 단계

[단원 12: Excel에서 분석](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)합니다.

  
  
