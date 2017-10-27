---
title: "단계별된 보고서 (보고서 작성기 및 SSRS) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 232b8e03dc8e5e2130d127408f356ba2dc0492d5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>단계별 보고서 만들기(보고서 작성기 및 SSRS)
단계별 보고서는 아래 예제와 같이 동일한 열의 부모 그룹 아래에 들여 쓴 정보 행 또는 자식 그룹을 표시하는 페이지가 매겨진  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서의 한 유형입니다.  
  
 ![렌더링 된 단계별된 보고서](../../reporting-services/report-design/media/steppedreportrendered.gif "렌더링 된 보고서도 실행")  
  
 기존 테이블 보고서에서는 부모 그룹이 보고서의 인접 열에 배치됩니다. 새로운 테이블릭스 데이터 영역을 사용하면 그룹과 정보 행 또는 자식 그룹을 동일한 열에 추가할 수 있습니다. 그룹 행을 정보 행 또는 자식 그룹 행과 구별하기 위해 글꼴 색과 같은 서식을 적용하거나 정보 행을 들여쓸 수 있습니다.  
  
 이 항목의 절차에서는 단계별 보고서를 수동으로 만드는 방법을 보여 줍니다. 여기서 설명하는 방법 대신 새 테이블 또는 행렬 마법사를 사용할 수도 있습니다. 이 마법사를 사용하면 단계별 보고서의 레이아웃이 기본 제공되므로 보고서를 쉽게 만들 수 있습니다. 마법사를 완료한 후 보고서의 레이아웃을 추가로 조정할 수 있습니다.  
  
> [!NOTE]  
>  마법사는 보고서 작성기에서만 사용할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-stepped-report"></a>단계별 보고서를 만들려면  
  
1.  테이블 보고서를 만듭니다. 예를 들어 테이블릭스 데이터 영역을 삽입하고 데이터 행에 필드를 추가합니다.  
  
2.  보고서에 부모 그룹을 추가합니다.  
  
    1.  테이블의 아무 곳이나 클릭하여 선택합니다. 그룹화 창의 행 그룹 창에 그룹 세부 정보가 표시됩니다.  
  
    2.  그룹화 창에서 그룹 세부 정보를 마우스 오른쪽 단추로 클릭하고 **그룹 추가**를 가리킨 다음 **부모 그룹**을 클릭합니다.  
  
    3.  **테이블릭스 그룹** 대화 상자에서 그룹의 이름을 제공하고 그룹 식을 드롭다운 목록에서 선택하거나 입력합니다. 드롭다운 목록에는 보고서 데이터 창에서 사용할 수 있는 간단한 필드 식이 표시됩니다. 예를 들어 [PostalCode]는 데이터 집합의 PostalCode 필드에 대한 간단한 필드 식입니다.  
  
    4.  **그룹 머리글 추가**를 선택합니다. 이 옵션은 그룹 위에 그룹 레이블과 그룹 합계를 위한 정적 행을 추가합니다. 이와 마찬가지로 **그룹 바닥글 추가** 를 선택하여 그룹 아래에 정적 행을 추가할 수 있습니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     이제 기본적인 테이블 형식 보고서가 준비되었습니다. 이 보고서를 렌더링하면 그룹 인스턴스 값이 들어 있는 한 개의 열과 그룹으로 묶은 정보 데이터가 들어 있는 한 개 이상의 열이 표시됩니다. 다음 그림에서는 디자인 화면의 데이터 영역을 보여 줍니다.  
  
     ![테이블 데이터 영역의 그룹과](../../reporting-services/report-design/media/tabledataregionwithgroup.gif "그룹을 사용 하 여 테이블 데이터 영역")  
  
     다음 그림에서는 보고서를 볼 때의 렌더링된 데이터 영역을 보여 줍니다.  
  
     ![렌더링 된 그룹화 된 보고서](../../reporting-services/report-design/media/tablereportrendered.gif "렌더링 된 보고서 그룹화")  
  
3.  단계별 보고서의 경우 그룹 인스턴스를 표시하는 첫 번째 열이 필요하지 않습니다. 대신 그룹 머리글 셀의 값을 복사하고 그룹 열을 삭제한 다음 그룹 머리글 행의 첫 번째 입력란에 붙여넣습니다. 그룹 열을 제거하려면 그룹 열 또는 셀을 마우스 오른쪽 단추로 클릭하고 **열 삭제**를 클릭합니다. 다음 그림에서는 디자인 화면의 데이터 영역을 보여 줍니다.  
  
     ![그룹 머리글 행을 사용 하 여 데이터 영역](../../reporting-services/report-design/media/tabledataregiongroupheader.gif "그룹 머리글 행을 사용 하 여 데이터 영역")  
  
4.  정보 행을 동일한 열의 그룹 머리글 행 아래 들여 쓰려면 정보 데이터 셀의 안쪽 여백을 변경합니다.  
  
    1.  들여 쓰려는 정보 필드가 포함된 셀을 선택합니다. 해당 셀의 입력란 속성이 속성 창에 나타납니다.  
  
    2.  속성 창의 **맞춤**에서 **안쪽 여백**의 속성을 확장합니다.  
  
    3.  **왼쪽**에 **.5in**등의 새 안쪽 여백 값을 입력합니다. 안쪽 여백은 지정된 값만큼 셀의 텍스트를 들여씁니다. 기본 안쪽 여백은 2포인트입니다. 안쪽 여백 속성의 올바른 값은 0 또는 양수를 입력하고 그 뒤에 크기 단위 지정자를 입력한 값입니다.  
  
         사용할 수 있는 크기 단위 지정자는 다음과 같습니다.  
  
        |||  
        |-|-|  
        |**in**|인치(1인치 = 2.54센티미터)|  
        |**cm**|센티미터|  
        |**MM**|밀리미터|  
        |**pt**|포인트(1포인트 = 1/72인치)|  
        |**pc**|파이카(1파이카 = 12포인트)|  
  
     데이터 영역은 다음 예와 비슷한 모양이 됩니다.  
  
     ![단계별된 보고서에 대 한 데이터 영역](../../reporting-services/report-design/media/steppedreportdataregion.gif "단계별된 보고서에 대 한 데이터 영역")  
  
     **단계별 보고서 레이아웃의 데이터 영역**  
  
     **홈** 탭에서 **실행**을 클릭합니다. 보고서에 자식 그룹 값에 대해 들여쓴 수준으로 그룹이 표시됩니다.  
  
## <a name="to-create-a-stepped-report-with-multiple-groups"></a>그룹이 여러 개인 단계별 보고서를 만들려면  
  
1.  이전 절차에 설명된 대로 보고서를 만듭니다.  
  
2.  보고서에 다른 그룹을 더 추가합니다.  
  
    1.  행 그룹 창에서 그룹을 마우스 오른쪽 단추로 클릭하고 **그룹 추가**를 클릭한 다음 추가할 그룹 유형을 선택합니다.  
  
        > [!NOTE]  
        >  데이터 영역에 그룹을 추가하는 데는 여러 가지 방법이 있습니다. 자세한 내용은 [데이터 영역에서 그룹 추가 또는 삭제&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)를 참조하세요.  
  
    2.  **테이블릭스 그룹** 대화 상자에서 이름을 입력합니다.  
  
    3.  **그룹 식**에서 식을 입력하거나 그룹화할 데이터 집합 필드를 선택합니다. 식을 만들려면 식 단추(**fx**)를 클릭하여 **식** 대화 상자를 엽니다.  
  
    4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  그룹 데이터를 표시하는 셀의 안쪽 여백을 변경합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [페이지 머리글 및 바닥글 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [보고서 항목 서식 지정 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [테이블 릭 스 데이터 영역 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [테이블 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [행렬 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [목록 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

