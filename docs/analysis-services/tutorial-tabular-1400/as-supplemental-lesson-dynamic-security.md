---
title: 'Analysis Services tutorial 추가 단원: 동적 보안 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: 2e5fd35b35a61e7844808e7fff053d6fb7a0434b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045467"
---
# <a name="supplemental-lesson---dynamic-security"></a>추가 단원-동적 보안

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 추가 단원에서는 동적 보안을 구현 하는 추가 역할을 만듭니다. 동적 보안은 현재 로그온한 사용자의 사용자 이름 또는 로그인 ID를 기반으로 하는 행 수준 보안을 제공합니다. 
  
동적 보안을 구현 하려면 모델에 연결 하 고 모델 개체와 데이터를 찾아볼 수 있는 사용자의 사용자 이름이 포함 된 모델에 테이블을 추가 합니다. 이 자습서를 사용 하 여 만드는 모델은 Adventure Works;의 컨텍스트에서 실행 그러나이 단원을 완료 하려면 사용자의 도메인에서 사용자가 포함 하는 테이블을 추가 해야 합니다. 추가 된 사용자 이름에 대 한 암호 필요가 없습니다. 사용자의 도메인에서 사용자의 작은 샘플으로는 EmployeeSecurity 테이블을 만들려면는 붙여넣기 기능을 사용 데이터를 Excel 스프레드시트에서 합니다. 실제 시나리오에서는 사용자 이름이 포함 된 테이블 일반적으로 것 실제 데이터베이스에서 테이블을 데이터 소스로 예를 들어는 실제 DimEmployee 테이블입니다.  
  
동적 보안을 구현 하려면 두 개의 DAX 함수를 사용 하면: [USERNAME 함수 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) 및 [LOOKUPVALUE 함수 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)합니다. 행 필터 수식에서 적용되는 이 함수는 새 역할에서 정의됩니다. LOOKUPVALUE 함수를 사용 하 여 수식을 EmployeeSecurity 테이블의 값을 지정 합니다. 수식 로그온 한 사용자의 사용자 이름을 지정 하는 사용자 이름 함수에 값이이 역할에 속해 있는지를 전달 합니다. 그런 다음 사용자는 역할의 행 필터에 지정된 데이터만 검색할 수 있습니다. 이 시나리오에서는 영업 직원이 이들이 속한은 영업 지역에 대 한 인터넷 매출 데이터를 찾아볼 수만 지정 합니다.  
  
이러한 태스크는 이 Adventure Works 테이블 형식 모델 시나리오에 해당되는 것이며 실제 시나리오에 반드시 적용되는 것은 아닙니다. 각 태스크에는 태스크의 목적을 설명하는 추가 정보가 포함되어 있습니다.  
  
이 단원에 소요되는 예상 시간: **30분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 추가 단원은 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 추가 단원의 태스크를 수행하려면 이전 단원을 모두 완료해야 합니다.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>dimSalesTerritory 테이블을 AW Internet Sales Tabular Model 프로젝트에 추가합니다.  

이 Adventure Works 시나리오에 대 한 동적 보안을 구현 하려면 모델에 두 개의 추가 테이블을 추가 해야 합니다. 추가한 첫 번째 테이블은 동일한 AdventureWorksDW 데이터베이스의 DimSalesTerritory (Sales Territory) 됩니다. 나중에 로그온된 한 사용자를 찾아볼 수는 특정 데이터를 정의 하는 SalesTerritory 테이블에 행 필터를 적용 합니다.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>dimSalesTerritory 테이블을 추가하려면  
  
1.  테이블 형식 모델 탐색기에서 > **데이터 원본**해당 연결을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **새 테이블 가져오기를**합니다.  

    가장 자격 증명 대화 상자가 나타나면 2단원: 데이터 추가에서 사용한 가장 자격 증명을 입력합니다.
  
2.  탐색 창의 선택 된 **DimSalesTerritory** 테이블을 마우스 클릭 **확인**합니다.    
  
3.  쿼리 편집기에서 클릭는 **DimSalesTerritory** 쿼리하고 다음 제거 **SalesTerritoryAlternateKey** 열입니다.  
  
7.  **가져오기**를 클릭합니다.  
  
    새 테이블이 모델 작업 영역에 추가 됩니다. 그런 다음 원본 DimSalesTerritory 테이블의 개체와 데이터 AW Internet Sales Tabular Model으로 가져옵니다.  
  
9. 테이블을 성공적으로 가져온 후 클릭 **닫기**합니다.  

## <a name="add-a-table-with-user-name-data"></a>사용자 이름 데이터가 있는 테이블 추가  

AdventureWorksDW 예제 데이터베이스의 DimEmployee 테이블 AdventureWorks 도메인의 사용자가 포함 합니다. 해당 사용자 이름은 사용자 환경에 존재 하지 않습니다. 조직의 실제 사용자 (3 개 이상) 작은 예제가 포함 된 모델에 테이블을 만들어야 합니다. 구성원으로 이러한 사용자 새 역할에 추가 합니다. 사용자의 도메인에서 실제 Windows 사용자 이름이 필요는 없지만 샘플 사용자 이름의 암호 필요가 없습니다.  
  
#### <a name="to-add-an-employeesecurity-table"></a>EmployeeSecurity 테이블을 추가 하려면  
  
1.  Microsoft Excel에서 워크시트를 만드는 엽니다.  
  
2.  머리글 행이 포함된 다음 테이블을 복사한 다음 워크시트에 붙여 넣습니다.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  이름 및 조직에 있는 세 개의 사용자의 로그인 id와 이름, 성 및 domain\username을 대체 합니다. 이 사용자가 둘 이상의 영업 지역에 속한 보여 주는 EmployeeId 1에 대 한 처음 두 행에 동일한 사용자를 포함 합니다. EmployeeId 및 SalesTerritoryId 필드 그대로 둡니다.  
  
4.  워크시트를로 저장 **SampleEmployee**합니다.  
  
5.  워크시트에서 머리글을 포함 하 여 직원 데이터가 있는 모든 셀을 선택 하 고 선택한 데이터를 마우스 오른쪽 단추로 클릭 한 다음 **복사**합니다.  
  
6.  SSDT에서는 클릭는 **편집** 메뉴를 차례로 클릭 **붙여넣기**합니다.  
  
    붙여넣기가 회색 모델 디자이너 창에 있는 테이블의 모든 열을 클릭 하 고 다시 시도 하십시오.  
  
7.  에 **붙여넣기 미리 보기** 대화 상자의 **테이블 이름**, 형식 **EmployeeSecurity**합니다.  
  
8.  **붙여 넣을 데이터**, 모든 사용자 데이터 및 SampleEmployee 워크시트에서 헤더를 포함 하는 데이터를 확인 합니다.  
  
9. **첫 행을 열 머리글로 사용** 이 선택되어 있는지 확인한 다음 **확인**을 클릭합니다.  
  
    SampleEmployee 워크시트에서 복사 된 직원 데이터가 있는 EmployeeSecurity 라는 새 테이블이 생성 됩니다.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>FactInternetSales, DimGeography, 및 DimSalesTerritory 테이블 간의 관계 만들기  

모든 FactInternetSales, DimGeography, 및 DimSalesTerritory 테이블 SalesTerritoryId 공통 된 열을 포함 합니다. DimSalesTerritory 테이블의 SalesTerritoryId 열 각 영업 지역에 대해 다른 Id 사용 하 여 값을 포함합니다.  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>FactInternetSales, DimGeography, 및 DimSalesTerritory 테이블 간의 관계를 만들려면  
  
1.  다이어그램 뷰에서는 **DimGeography** 테이블을 클릭 한 채로 **SalesTerritoryId** 열을 다음 커서를 끌어는 **SalesTerritoryId** 열에는 **DimSalesTerritory** 테이블을 마우스를 놓습니다.  
  
2.  에 **FactInternetSales** 테이블을 클릭 한 채로 **SalesTerritoryId** 열에서 다음 커서를 끌어는 **SalesTerritoryId** 열에는 **DimSalesTerritory** 테이블을 마우스를 놓습니다.  
  
    이 관계의 활성 속성은 False, 되지 않음입니다. FactInternetSales 테이블에 다른 활성 관계가 이미 있습니다.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>클라이언트 응용 프로그램에서 EmployeeSecurity 테이블 숨기기  

이 태스크에서는 숨기면 EmployeeSecurity 테이블 지속적으로 업데이트를 클라이언트 응용 프로그램의 필드 목록에 표시 합니다. 테이블 숨기기 보호 하지 않습니다는 염두에 둬야 합니다. 사용자가 알고 있는 경우 EmployeeSecurity 테이블 데이터를 쿼리할 여전히 수 방법입니다. 사용자가 데이터를 쿼리할 수 없도록 방지 EmployeeSecurity 테이블 데이터를 보호 하려면 이후 태스크에서 필터를 적용 합니다.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>클라이언트 응용 프로그램에서 EmployeeSecurity 테이블을 숨기려면  
  
-   모델 디자이너의 다이어그램 뷰에서 **Employee** 테이블 머리글을 마우스 오른쪽 단추로 클릭한 다음 **클라이언트 도구에서 숨기기**를 클릭합니다.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할 만들기  

이 태스크에서는 사용자 역할을 만듭니다. 이 역할 정의 DimSalesTerritory 테이블의 어떤 행이 사용자가 볼 수 있는 행 필터를 포함 합니다. 필터는 DimSalesTerritory와 관련 된 다른 모든 테이블에 일 대 다 관계 방향으로 적용 됩니다. 역할의 구성원 인 모든 사용자가 쿼리할 수 없도록 전체 EmployeeSecurity 테이블의 보안을 유지 하는 필터를 적용할 수도 있습니다.  
  
> [!NOTE]  
> 이 단원에서 만드는 Sales Employees by Territory 역할은 멤버가 자신이 속한 영업 지역에 대한 판매 데이터만 검색(또는 쿼리)할 수 있도록 제한합니다. 에 추가한 경우 사용자를 멤버로 Sales Employees by Territory 역할에서 만든 역할의 멤버로 존재 [11 단원: 역할 만들기](../tutorial-tabular-1400/as-lesson-11-create-roles.md), 사용 권한의 조합의 얻을 합니다. 사용자가 여러 역할의 멤버인 경우 각 역할에 대해 정의된 사용 권한과 행 필터는 누적됩니다. 즉, 사용자는 더 큰 권한이 역할의 조합으로 결정 합니다.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할을 만들려면  
  
1.  SSDT에서는 클릭는 **모델** 메뉴를 차례로 클릭 **역할**합니다.  
  
2.  **역할 관리자**, 클릭 **새로**합니다.  
  
    없음 권한을 가진 새 역할이 목록에 추가됩니다.  
  
3.  새 역할을 클릭 한 다음는 **이름** 열을 역할 이름 바꾸기 **Sales Employees by Territory**합니다.  
  
4.  **사용 권한** 열에서 드롭다운 목록을 클릭한 다음 **읽기** 권한을 선택합니다.  
  
5.  클릭는 **멤버** 탭을 클릭 한 다음 **추가**합니다.  
  
6.  에 **사용자 또는 그룹 선택** 대화 상자의 **에서 선택할 개체 이름을 입력**, EmployeeSecurity 테이블을 만들 때 사용한 첫 번째 예제 사용자 이름을 입력 합니다. **이름 확인** 을 클릭하여 사용자 이름이 올바른지 확인한 다음 **확인**을 클릭합니다.  
  
    EmployeeSecurity 테이블을 만들 때 사용한 다른 예제 사용자 이름을 추가 하는이 단계를 반복 합니다.  
  
7.  클릭는 **행 필터** 탭 합니다.  
  
8.  에 대 한는 **EmployeeSecurity** 의 테이블는 **DAX 필터** 열에서 다음 수식을 입력 합니다.  
  
    ```
      =FALSE()  
    ```
  
    이 수식은 false 부울 조건 변환할 모든 열을 지정 합니다. EmployeeSecurity 테이블에 대 한 열이 없습니다 by Territory 사용자 역할 판매 직원의 멤버가 쿼리할 수 있습니다.  
  
9. 에 대 한는 **DimSalesTerritory** 테이블에서 다음 수식을 입력 합니다.  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    이 수식에서 LOOKUPVALUE 함수는 여기서 EmployeeSecurity [LoginId]는 현재 Windows 사용자 이름 로그온과 동일 하 고 [SalesTerritoryId] EmployeeSecurity DimSalesTerritory [SalesTerritoryId]와 같습니다 DimEmployeeSecurity [SalesTerritoryId] 열에 대 한 모든 값을 반환 합니다.  
  
    DimSalesTerritory 테이블에 표시 된 행을 제한 하 영업 지역 Id가 LOOKUPVALUE에서 반환 된 집합이 사용 됩니다. LOOKUPVALUE 함수에서 반환 된 Id의 집합에는 행에 대 한 SalesTerritoryID 인 행만 표시 됩니다.  
  
10. 역할 관리자에서 클릭 **확인**합니다.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할 테스트  

이 작업을 by Territory 사용자 역할에는 판매 직원의 효율성을 테스트할 SSDT에서 Excel 기능에서 분석을 사용 합니다. 역할의 멤버 이며 EmployeeSecurity 테이블에 추가 된 사용자 이름 중 하나를 지정 합니다. 이 사용자 이름은 Excel과 모델 간에 만들어진 연결에서 유효 사용자 이름으로 다음 사용 됩니다.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Sales Employees by Territory 사용자 역할을 테스트하려면  
  
1.  SSDT에서는 클릭는 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.  
  
2.  **Excel에서 분석** 대화 상자의 **모델에 연결하기 위해 사용할 사용자 이름 또는 역할 지정**에서 **기타 Windows 사용자**를 선택한 다음 **찾아보기**를 클릭합니다.  
  
3.  에 **사용자 또는 그룹 선택** 대화 상자의 **선택할 개체 이름을 입력**EmployeeSecurity 테이블에 포함 된 사용자 이름을 입력 한 다음 클릭 **이름 확인**합니다.  
  
4.  **확인** 을 클릭하여 **사용자 또는 그룹 선택** 대화 상자를 닫은 다음 **확인** 을 클릭하여 **Excel에서 분석** 대화 상자를 닫습니다.  
  
    새 통합 문서와 Excel이 열립니다. 피벗 테이블을 자동으로 만들어집니다. 피벗 테이블 필드 목록에 새 모델에서 사용할 수 있는 데이터 필드 대부분 포함 되어 있습니다.  
  
    공지 EmployeeSecurity 테이블 피벗 테이블 필드 목록에 표시 되지 않습니다. 이전 작업에서 클라이언트 도구에서이 테이블을 숨긴 것입니다.  
  
5.  에 **필드** 목록에서 **∑ Internet Sales** (측정값)을 선택 된 **InternetTotalSales** 측정값입니다. 측정값에 입력 된는 **값** 필드입니다.  
  
6.  선택 된 **SalesTerritoryId** 열에서는 **DimSalesTerritory** 테이블입니다. 열에 입력 된는 **행 레이블** 필드입니다.  
  
    인터넷 판매 수치는 사용한 유효 사용자 이름이 속하는 한 지역에 대해서만 나타납니다. 행 레이블 필드로 DimGeography 테이블에서 도시와 같은 다른 열을 선택 하면 유효 사용자가 속한 영업 지역의 도시만 표시 됩니다.  
    이 사용자는 이동 하거나 자신이 속한 이외의 다른 지역에 대 한 모든 인터넷 판매 데이터를 쿼리할 수 없습니다. 이 제한은 DimSalesTerritory 테이블 Sales Employees by Territory 사용자 역할에에서는 다른 영업 지역에 관련 된 모든 데이터에 대 한 데이터를 보호에 대해 행 필터 정의 하기 때문에입니다.  
  
## <a name="see-also"></a>관련 항목:  

[USERNAME 함수 (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 함수 (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 함수 (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
