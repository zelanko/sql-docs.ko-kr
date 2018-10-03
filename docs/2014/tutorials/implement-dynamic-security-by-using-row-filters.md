---
title: 행 필터를 사용 하 여 동적 보안 구현 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 8bf03c45-caf5-4eda-9314-e4f8f24a159f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7fa34786d8d939581c5b8fecfb54103229a2a2c8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196583"
---
# <a name="implement-dynamic-security-by-using-row-filters"></a>행 필터를 사용하여 동적 보안 구현
  이 추가 단원에서는 동적 보안을 구현하는 추가 역할을 만들어 봅니다. 동적 보안은 현재 로그온한 사용자의 사용자 이름 또는 로그인 ID를 기반으로 하는 행 수준 보안을 제공합니다. 자세한 내용은 [역할&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/roles-ssas-tabular.md)을 참조하세요.  
  
 동적 보안을 구현하려면 데이터 원본인 모델에 대해 연결을 만들고 모델 개체와 데이터를 찾아볼 수 있는 사용자의 Windows 사용자 이름이 포함된 테이블을 모델에 추가해야 합니다. 이 자습서를 사용하여 만드는 모델은 Adventure Works Corp.의 컨텍스트에 있지만 이 단원을 완료하려면 자체 도메인의 사용자가 포함된 테이블을 추가해야 합니다. 추가할 사용자 이름의 암호는 필요 없습니다. 해당 도메인의 일부 사용자 예제를 사용하여 Employee Security 테이블을 만들려면 붙여넣기 기능을 사용하여 Excel 스프레드시트의 데이터를 붙여 넣습니다. 실제 시나리오에서 모델에 추가하는 사용자 이름이 포함된 테이블은 일반적으로 실제 데이터베이스의 테이블을 데이터 원본으로 사용합니다(예: 실제 dimEmployee 테이블).  
  
 동적 보안을 구현 하기 위해 두 개의 새 DAX 함수인 사용할지: [USERNAME 함수 &#40;DAX&#41; ](https://msdn.microsoft.com/library/hh230954.aspx) 하 고 [LOOKUPVALUE 함수 &#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx). 행 필터 수식에서 적용되는 이 함수는 새 역할에서 정의됩니다. 이 수식은 LOOKUPVALUE 함수를 사용하여 Employee Security 테이블의 값을 지정한 다음 이 값을 USERNAME 함수에 전달하며, 이 함수는 로그온한 사용자의 사용자 이름이 이 역할에 속하도록 지정합니다. 그런 다음 사용자는 역할의 행 필터에 지정된 데이터만 검색할 수 있습니다. 이 시나리오에서는 영업 직원이 자신이 멤버로 속한 영업 지역에 대한 인터넷 매출 데이터만 찾아볼 수 있도록 지정합니다.  
  
 이 추가 단원을 완료하기 위해 일련의 태스크를 완료합니다. 이러한 태스크는 이 Adventure Works 테이블 형식 모델 시나리오에 해당되는 것이며 실제 시나리오에 반드시 적용되는 것은 아닙니다. 각 태스크에는 태스크의 목적을 설명하는 추가 정보가 포함되어 있습니다.  
  
 이 단원에 소요되는 예상 시간: **30분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 추가 단원 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원의 태스크를 수행하려면 이전 단원을 모두 완료해야 합니다.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>dimSalesTerritory 테이블을 AW Internet Sales Tabular Model 프로젝트에 추가합니다.  
 이 Adventure Works 시나리오에 대한 동적 보안을 구현하려면 두 개의 추가 테이블을 모델에 추가해야 합니다. 추가할 첫 번째 테이블은 동일한 AdventureWorksDW 데이터베이스의 dimSalesTerritory(Sales Territory)입니다. 나중에 로그온한 사용자가 검색할 수 있는 특정 데이터를 정의하는 Sales Territory 테이블에 행 필터를 적용합니다.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>dimSalesTerritory 테이블을 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **기존 연결**을 클릭합니다.  
  
2.  **기존 연결** 대화 상자에서 **Adventure Works DB from SQL** 데이터 원본 연결이 선택되어 있는지 확인한 다음 **열기**를 클릭합니다.  
  
     가장 자격 증명 대화 상자가 나타나면 2단원: 데이터 추가에서 사용한 가장 자격 증명을 입력합니다.  
  
3.  **데이터를 가져오는 방법 선택** 페이지에서 **데이터를 가져올 테이블 및 뷰를 목록에서 선택** 을 선택된 상태로 두고 **다음**을 클릭합니다.  
  
4.  **테이블 및 뷰 선택** 페이지에서 **DimSalesTerritory** 테이블을 선택합니다.  
  
5.  이름 열에 **Sales Territory**를 입력합니다.  
  
6.  **미리 보기 및 필터**를 클릭합니다.  
  
7.  **SalesTerritoryAlternateKey** 열을 선택 취소한 다음 **확인**을 클릭합니다.  
  
8.  **테이블 및 뷰 선택** 페이지에서 **마침**을 클릭합니다.  
  
     새 테이블이 모델 작업 영역에 추가됩니다. 그런 다음 원본 dimSalesTerritory 테이블의 개체와 데이터를 AW Internet Sales Tabular Model의 새 Sales Territory 테이블에 가져옵니다.  
  
9. 테이블을 가져온 후 **닫기**를 클릭합니다.  
  
## <a name="give-the-columns-friendly-names"></a>열에 이름 지정  
 이 태스크에서는 Sales Territory 테이블의 열에 이름을 지정합니다. 테이블 및/또는 열에 항상 이름을 지정할 필요가 있는 것은 아니지만, 이렇게 하면 모델 디자이너에서 모델 프로젝트를 보다 쉽게 탐색할 수 있을 뿐만 아니라 사용자가 클라이언트 응용 프로그램 필드 목록에서 모델 개체 및 데이터를 쉽게 찾아볼 수 있습니다.  
  
#### <a name="to-rename-columns-in-the-sales-territory-table"></a>Sales Territory 테이블에서 열의 이름을 바꾸려면  
  
-   모델 디자이너의 **Sales Territory** 테이블에서 열의 이름을 다음과 같이 바꿉니다.  
  
     **Sales Territory**  
  
    |원본 이름|이름|  
    |-----------------|-------------------|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesTerritoryRegion|Sales Territory Region|  
    |SalesTerritoryCountry|Sales Territory Country|  
    |SalesTerritoryGroup|Sales Territory Group|  
  
## <a name="add-a-table-with-user-name-data"></a>사용자 이름 데이터가 있는 테이블 추가  
 AdventureWorksDW 예제 데이터베이스의 dimEmployee 테이블에는 AdventureWorks 도메인의 사용자가 포함되고 해당 사용자 이름은 사용자 환경에 존재하지 않기 때문에 사용자 조직의 실제 사용자(3명)로 이루어진 작은 예제가 포함된 테이블을 모델에서 만들어야 합니다. 그런 다음 이 사용자를 새 역할에 멤버로 추가합니다. 샘플 사용자 이름의 암호는 필요 없지만 자체 도메인의 실제 Windows 사용자 이름이 필요합니다.  
  
#### <a name="to-add-an-employee-security-table"></a>Employee Security 테이블을 추가하려면  
  
1.  Microsoft Excel을 열고 새 워크시트를 만듭니다.  
  
2.  머리글 행이 포함된 다음 테이블을 복사한 다음 워크시트에 붙여 넣습니다.  
  
    |Employee Id|Sales Territory Id|First Name|Last Name|Login Id|  
    |-----------------|------------------------|----------------|---------------|--------------|  
    |1|2|\<사용자 이름 >|\<마지막 사용자 이름 >|\<도메인 \ 사용자 이름 >|  
    |1|3|\<사용자 이름 >|\<마지막 사용자 이름 >|\<도메인 \ 사용자 이름 >|  
    |2|4|\<사용자 이름 >|\<마지막 사용자 이름 >|\<도메인 \ 사용자 이름 >|  
    |3|5|\<사용자 이름 >|\<마지막 사용자 이름 >|\<도메인 \ 사용자 이름 >|  
  
3.  새 워크시트에서 이름, 성 및 domain\username을 사용자 조직에 있는 사용자 세 명의 이름과 로그인 ID로 바꿉니다. Employee Id 1의 처음 두 행에 동일한 사용자 이름을 입력합니다. 이렇게 하면 사용자가 두 개 이상의 영업 지역에 속해 있음을 표시할 수 있습니다. Employee Id 및 Sales Territory Id 필드를 그대로 둡니다.  
  
4.  워크시트를로 저장 `Sample Employee`합니다.  
  
5.  워크시트에서 머리글을 포함하여 직원 데이터가 있는 모든 셀을 선택하고 선택한 데이터를 마우스 오른쪽 단추로 클릭한 다음 **복사**를 클릭합니다.  
  
6.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **편집** 메뉴를 클릭한 다음 **붙여넣기**를 클릭합니다.  
  
     붙여넣기가 회색으로 나타나는 경우 모델 디자이너 창의 테이블에서 열을 클릭하고 **편집** 메뉴를 클릭한 다음 **붙여넣기**를 클릭합니다.  
  
7.  에 **붙여넣기 미리 보기** 대화 상자의 **테이블 이름**, 형식 `Employee Security`합니다.  
  
8.  **붙여넣을 데이터**에서 Sample Employee 워크시트의 사용자 데이터와 머리글이 모두 포함되어 있는지 확인합니다.  
  
9. **첫 행을 열 머리글로 사용** 이 선택되어 있는지 확인한 다음 **확인**을 클릭합니다.  
  
     Sample Employee 워크시트에서 복사된 직원 데이터를 포함하는 Employee Security라는 새 테이블이 만들어집니다.  
  
## <a name="create-relationships-between-internet-sales-geography-and-sales-territory-table"></a>Internet Sales, Geography 및 Sales Territory 테이블 간의 관계 만들기  
 Internet Sales, Geography 및 Sales Territory 테이블에는 모두 Sales Territory Id라는 공통의 열이 포함됩니다. Sales Territory 테이블의 Sales Territory Id 열에는 각 영업 지역에 대해 다른 ID인 값이 들어 있습니다.  
  
#### <a name="to-create-relationships-between-the-internet-sales-geography-and-the-sales-territory-table"></a>Internet Sales, Geography 및 Sales Territory 테이블 간의 관계를 만들려면  
  
1.  모델 디자이너의 다이어그램 뷰에 있는 **Geography** 테이블에서 **Sales Territory Id** 열을 클릭한 채로 커서를 **Sales Territory** 테이블의 **Sales Territory Id** 열로 끌어다 놓습니다.  
  
2.  **Internet Sales** 테이블에서 **Sales Territory Id** 열을 클릭한 채로 커서를 **Sales Territory** 테이블의 **Sales Territory Id** 열로 끌어다 놓습니다.  
  
     이 관계의 활성 속성은 False이므로 비활성입니다. Internet Sales 테이블에는 측정값에서 사용되는 다른 활성 관계가 이미 있기 때문입니다.  
  
## <a name="hide-the-employee-security-table-from-client-applications"></a>클라이언트 응용 프로그램에서 Employee Security 테이블 숨기기  
 이 태스크에서는 클라이언트 응용 프로그램의 필드 목록에 나타나지 않도록 Employee Security 테이블을 숨깁니다. 테이블 숨기더라도 테이블이 안전하게 보호되는 것은 아닙니다. 방법을 아는 경우 사용자는 여전히 Employee Security 테이블 데이터를 쿼리할 수 있습니다. 사용자가 데이터를 쿼리할 수 없도록 Employee Security 테이블 데이터를 안전하게 보호하려면 이후 태스크에서 필터를 적용합니다.  
  
#### <a name="to-hide-the-employee-table-from-client-applications"></a>클라이언트 응용 프로그램에서 Employee 테이블을 숨기려면  
  
-   모델 디자이너의 다이어그램 뷰에서 **Employee** 테이블 머리글을 마우스 오른쪽 단추로 클릭한 다음 **클라이언트 도구에서 숨기기**를 클릭합니다.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할 만들기  
 이 태스크에서는 새 사용자 역할을 만듭니다. 이 역할에는 Sales Territory 테이블에서 사용자에게 표시되지 않는 행을 정의하는 행 필터가 포함됩니다. 그러면 이 필터는 일대다 관계 방향으로 Sales Territory에 관련된 다른 모든 테이블에 적용됩니다. 역할의 멤버인 사용자가 전체 Employee Security 테이블을 쿼리할 수 없도록 보호하는 간단한 필터도 적용합니다.  
  
> [!NOTE]  
>  이 단원에서 만드는 Sales Employees by Territory 역할은 멤버가 자신이 속한 영업 지역에 대한 판매 데이터만 검색(또는 쿼리)할 수 있도록 제한합니다. [12단원: 역할 만들기](../analysis-services/lesson-11-create-roles.md)에서 만든 역할의 멤버로도 존재하는 사용자를 Sales Employees by Territory 역할에 멤버로 추가하면 사용 권한의 조합을 얻을 수 있습니다. 사용자가 여러 역할의 멤버인 경우 각 역할에 대해 정의된 사용 권한과 행 필터는 누적됩니다. 즉, 사용자는 역할의 조합으로 결정되는 더 큰 사용 권한을 갖게 됩니다.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **역할**을 클릭합니다.  
  
2.  **역할 관리자** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     없음 권한을 가진 새 역할이 목록에 추가됩니다.  
  
3.  새 역할을 선택한 다음 클릭 합니다 **이름** 열에서 역할 이름 바꾸기 `Sales Employees by Territory`합니다.  
  
4.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **읽기** 권한을 선택합니다.  
  
5.  **멤버** 탭을 클릭한 다음 **추가**를 클릭합니다.  
  
6.  **사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름 입력**에 Employee Security 테이블을 만들 때 사용한 첫 번째 예제 사용자 이름을 입력합니다. **이름 확인**을 클릭하여 사용자 이름이 올바른지 확인한 다음 **확인**을 클릭합니다.  
  
     이 단계를 반복하여 Employee Security 테이블을 만들 때 사용한 다른 예제 사용자 이름을 추가합니다.  
  
7.  **행 필터** 탭을 클릭합니다.  
  
8.  에 대 한 합니다 `Employee Security` 테이블의 **DAX 필터** 열 다음 수식을 입력 합니다.  
  
     `=FALSE()`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
     이 수식은 모든 열이 false 부울 조건으로 확인되도록 지정합니다. 따라서 Sales Employees by Territory 사용자 역할의 멤버가 Employee Security 테이블의 행을 쿼리할 수 없습니다.  
  
9. **Sales Territory** 테이블에 대해 다음 수식을 입력합니다.  
  
     `='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 'Employee Security'[Login Id], USERNAME(), 'Employee Security'[Sales Territory Id], 'Sales Territory'[Sales Territory Id])`  
  
     수식 작성을 마쳤으면 Enter 키를 누릅니다.  
  
     이 수식에서 LOOKUPVALUE 함수는 Employee Security[Sales Territory Id] 열의 모든 값을 반환하며, 여기서 Employee Security[Login Id]는 현재 로그온한 Windows 사용자 이름과 동일하고 Employee Security[Sales Territory Id]는 Sales Territory[Sales Territory Id]와 동일합니다.  
  
     LOOKUPVALUE에서 반환된 Sales Territory ID 집합은 Sales Territory 테이블에 표시되는 행을 제한하는 데 사용됩니다. 행에 대한 Sales Territory ID가 LOOKUPVALUE 함수에서 반환된 ID 집합에 속하는 행만 표시됩니다.  
  
10. 역할 관리자 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할 테스트  
 이 태스크에서는 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]의 Excel에서 분석 기능을 사용하여 Sales Employees by Territory 사용자 역할의 효율성을 테스트합니다. 역할의 멤버이며 Employee Security 테이블에 추가한 사용자 이름 중 하나를 지정합니다. 그러면 이 사용자는 Excel과 모델 간에 만들어진 연결에서 유효 사용자 이름으로 사용됩니다.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할을 테스트하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 **모델** 메뉴를 클릭한 다음 **Excel에서 분석**을 클릭합니다.  
  
2.  **Excel에서 분석** 대화 상자의 **모델에 연결하기 위해 사용할 사용자 이름 또는 역할 지정**에서 **기타 Windows 사용자**를 선택한 다음 **찾아보기**를 클릭합니다.  
  
3.  **사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름 입력**에 Employee 테이블에 포함된 사용자 이름 중 하나를 입력한 다음 **이름 확인**을 클릭합니다.  
  
4.  **확인**을 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 닫은 다음 **확인**을 클릭하여 **Excel에서 분석** 대화 상자를 닫습니다.  
  
     새 통합 문서와 함께 Excel이 열립니다. 피벗 테이블은 자동으로 만들어집니다. 피벗 테이블 필드 목록에는 새 모델에서 사용할 수 있는 대부분의 데이터 필드가 포함되어 있습니다.  
  
     Employee Security 테이블은 피벗 테이블 필드 목록에 표시되지 않습니다. 이전 태스크에서 이 테이블을 클라이언트 도구에서 숨기도록 선택했기 때문입니다.  
  
5.  **피벗 테이블 필드** 목록의 **∑ Internet Sales** (측정값)에서 **Internet Total Sales** 측정값을 선택합니다. 이 측정값은 **값** 필드에 입력됩니다.  
  
6.  **피벗 테이블 필드** 목록의 **Sales Territory** 테이블에서 **Sales Territory Id** 열을 선택합니다. 이 열은 **행 레이블** 필드에 입력됩니다.  
  
     인터넷 판매 수치는 사용한 유효 사용자 이름이 속하는 한 지역에 대해서만 나타납니다. Geography table에서 다른 열(예: City)을 행 레이블 필드로 선택하면 유효 사용자가 속하는 영업 지역의 도시만 표시됩니다.  
  
     Sales Employees by Territory 사용자 역할에서 Sales Territory 테이블에 정의된 행 필터가 다른 영업 지역에 관련된 모든 데이터에 대한 데이터를 보호하기 때문에 이 사용자는 자신이 속한 지역 이외의 다른 지역에 대한 인터넷 판매 데이터를 검색하거나 쿼리할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [USERNAME 함수 &#40;DAX&#41;](https://msdn.microsoft.com/library/hh230954.aspx)   
 [LOOKUPVALUE 함수 &#40;DAX&#41;](https://msdn.microsoft.com/library/gg492170.aspx)   
 [CUSTOMDATA 함수 &#40;DAX&#41;](https://msdn.microsoft.com/library/hh213140.aspx)  
  
  
