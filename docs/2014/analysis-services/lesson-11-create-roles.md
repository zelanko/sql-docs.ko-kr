---
title: '12 단원: 역할 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 7c3b98fbbcbedca2a8bcdbefcd8e41e5d3d5c60b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080542"
---
# <a name="lesson-12-create-roles"></a>12단원: 역할 만들기
  이 단원에서는 역할을 만듭니다. 역할은 역할 멤버인 Windows 사용자로만 액세스를 제한함으로써 모델 데이터베이스 개체 및 데이터에 보안을 제공합니다. 각 역할은 없음, 읽기, 읽기 및 처리, 처리 또는 관리자라는 단일 사용 권한으로 정의됩니다. 모델을 제작하는 중에 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 역할 관리자 대화 상자를 사용하여 역할을 정의할 수 있습니다. 모델을 배포한 후 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 역할을 관리할 수 있습니다. 자세한 내용은 [역할&#40;SSAS 테이블 형식&#41;](tabular-models/roles-ssas-tabular.md)을 참조하세요.  
  
> [!NOTE]  
>  이 자습서를 완료하기 위해 역할을 만들 필요는 없습니다. 기본적으로 현재 로그인하는 데 사용한 계정에는 모델에 대한 관리자 권한이 있습니다. 그러나 조직의 다른 사용자가 보고 클라이언트 응용 프로그램을 통해 모델을 검색할 수 있도록 하려면 읽기 권한을 가진 역할을 하나 이상 만들어 해당 사용자를 멤버로 추가해야 합니다.  
  
 다음과 같은 세 개의 역할을 만듭니다.  
  
-   Sales Manager – 이 역할은 모든 모델 개체 및 데이터에 대한 읽기 권한을 할당할 조직의 사용자를 포함할 수 있습니다.  
  
-   Sales Analyst US – 이 역할은 미국 내 판매와 관련된 데이터만 검색할 수 있는 조직의 사용자를 포함할 수 있습니다. 이 역할에 대해 DAX 수식을 사용하여 멤버가 미국에 대한 데이터만 검색할 수 있도록 제한하는 *행 필터*를 정의합니다.  
  
-   Administrator – 이 역할은 관리자 권한을 할당해 무제한 액세스 및 사용 권한으로 model 데이터베이스에 대한 관리 태스크를 수행하도록 할 사용자를 포함할 수 있습니다.  
  
 조직의 Windows 사용자 및 그룹 계정은 고유하므로 특정 조직의 계정을 멤버에 추가할 수 있습니다. 그러나 이 자습서에서는 멤버를 비워둘 수도 있습니다. 나중에 12단원: Excel에서 분석에서 각 역할의 영향을 테스트할 수 있습니다.  
  
 이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [11단원: 파티션 만들기](lesson-10-create-partitions.md)를 완료해야 합니다.  
  
## <a name="create-roles"></a>역할 만들기  
  
#### <a name="to-create-a-sales-manager-user-role"></a>Sales Manager 사용자 역할을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할**을 클릭합니다.  
  
2.  **역할 관리자** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     없음 권한을 가진 새 역할이 목록에 추가됩니다.  
  
3.  새 역할을 선택한 다음 클릭은 **이름** 열을 역할 이름 바꾸기 `Internet Sales Manager`합니다.  
  
4.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **읽기** 권한을 선택합니다.  
  
5.  옵션: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.  
  
6.  **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
7.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>Sales Analyst US 사용자 역할을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할**을 클릭합니다.  
  
2.  **역할 관리자** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     없음 권한을 가진 새 역할이 목록에 추가됩니다.  
  
3.  새 역할을 선택한 다음 클릭은 **이름** 열을 역할 이름 바꾸기 `Internet Sales US`합니다.  
  
4.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **읽기** 권한을 선택합니다.  
  
5.  행 필터 탭을 클릭한 다음 **Geography** 테이블에 대해서만 DAX 필터 열에 다음 수식을 입력합니다.  
  
     `=Geography[Country Region Code] = "US"`  
  
     행 필터 수식은 부울(TRUE/FALSE) 값으로 확인되어야 합니다. 이 수식을 사용하면 Country Region Code 값이 "US"인 행만 사용자에게 표시되도록 지정됩니다.  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
6.  옵션: **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.  
  
7.  **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
8.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
#### <a name="to-create-an-administrator-role"></a>Administrator 역할을 만들려면  
  
1.  **역할 관리자** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
2.  새 역할을 선택한 다음 클릭은 **이름** 열을 역할 이름 바꾸기 `Internet Sales Administrator`합니다.  
  
3.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **관리자** 권한을 선택합니다.  
  
4.  **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.  
  
5.  옵션: **사용자 또는 그룹 선택** 대화 상자에서 역할에 포함할 조직의 Windows 사용자 또는 그룹을 입력합니다.  
  
6.  선택한 내용을 확인하고 **확인**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [13단원: Excel에서 분석](lesson-12-analyze-in-excel.md)으로 이동하세요.  
  
  