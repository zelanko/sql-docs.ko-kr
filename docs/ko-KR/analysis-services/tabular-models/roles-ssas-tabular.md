---
title: 역할 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c23948ae3a3326a6d8139b7e9556164108b9e1d6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="roles"></a>역할
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모델에서 역할은 모델에 대한 멤버 권한을 정의합니다. 역할의 멤버는 모델에 대해 역할 권한에 정의된 동작을 수행할 수 있습니다. 또한 읽기 권한을 갖도록 정의된 역할은 행 수준 필터를 사용하여 행 수준에서 추가적인 보안을 제공할 수 있습니다. 
  
 SQL Server Analysis Services에 대 한 역할에 Windows 사용자 이름 또는 Windows 그룹 및 사용 권한 (읽기, 프로세스, 관리자)을 통해 사용자 멤버가 포함 됩니다. Azure Analysis Services에 대 한 사용자가 Azure Active Directory와 사용자 이름 이어야 하며 조직 메일 주소 또는 UPN으로 지정 된 그룹 이어야 합니다. 
  
> [!IMPORTANT]  
>  사용자가 보고 클라이언트 응용 프로그램을 사용 하 여 배포 된 모델에 연결을 만들어야 합니다와 역할을 하나 이상 최소한 읽기 권한을 해당 사용자가 멤버입니다.  
  
 이 항목의 정보는 SSDT의 역할 관리자 대화 상자를 사용 하 여 역할을 정의 하는 테이블 형식 모델 작성자를 위한 것입니다. 모델을 작성하는 중에 정의된 역할은 모델 작업 영역 데이터베이스에 적용됩니다. Model 데이터베이스를 배포한 후에 모델 데이터베이스 관리자가 관리할 수 (추가, 편집, 삭제) SSMS를 사용 하 여 역할 멤버입니다. 배포 데이터베이스에서 역할의 멤버를 관리 하는 방법에 대 한 자세한 내용은 [테이블 형식 모델 역할](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_underst"></a> Understanding roles  
 역할은 모델 데이터 액세스를 관리 하려면 Analysis Services에서 사용 됩니다. 역할에는 다음과 같은 두 가지 유형이 있습니다.  
  
-   서버 역할-관리자 액세스는 Analysis Services 서버 인스턴스를 제공 하는 고정된 역할입니다.  
  
-   데이터베이스 역할 - 모델 작성자와 관리자가 관리자가 아닌 사용자의 model 데이터베이스 및 데이터 액세스를 제어하기 위해 정의한 역할  
  
 테이블 형식 모델에 대해 정의된 역할이 데이터베이스 역할입니다. 즉, 사용자가 구성 된 멤버를 포함 하는 역할 또는 권한이 그룹에 특정 동작을 정의 하는 해당 멤버는 모델 데이터베이스에 대해 수행할 수 있습니다. 데이터베이스 역할은 데이터베이스에서 별개의 개체로 생성되고, 해당 역할이 생성된 데이터베이스에만 적용됩니다. 사용자 및 그룹 역할에는 기본적으로 작업 영역 데이터베이스 서버에서 관리자 권한을 갖는 모델 작성자가 포함 됩니다. 관리자가 배포 된 모델입니다.  
  
 행 필터를 사용하여 테이블 형식 모델의 역할을 세부적으로 정의할 수 있습니다. 행 필터는 DAX 식을 사용하여 사용자가 쿼리할 수 있는 테이블의 행과 다양한 방향의 관련 행을 정의합니다. DAX 식을 사용하는 행 필터는 읽기 권한과 읽기 및 처리 권한에 대해서만 정의할 수 있습니다. 자세한 내용은 참고 [행 필터](#bkmk_rowfliters) 이 항목의 뒷부분에 나오는 합니다.  
  
 기본적으로 새 테이블 형식 모델 프로젝트를 만들 경우 모델 프로젝트에는 아무 역할도 없습니다. SSDT의 역할 관리자 대화 상자를 사용 하 여 역할을 정의할 수 있습니다. 모델 제작 중에 역할을 정의한 경우 해당 역할은 모델 작업 영역 데이터베이스에 적용됩니다. 모델을 배포하면 동일한 역할이 배포된 모델에 적용됩니다. 모델을 배포한 후 모델에 연결 된 역할 및 각 역할과 연결 된 SSMS를 사용 하 여 멤버 ([Analysis Services 관리자) 서버 역할 및 데이터베이스 관리자의 구성원이 관리할 수 있습니다.  
  
##  <a name="bkmk_permissions"></a> 사용 권한  
 결합된 읽기 및 처리 권한을 제외하고 역할별로 하나의 데이터베이스 권한이 정의되어 있습니다. 기본적으로 새 역할은 없음 권한을 갖게 됩니다. 즉, 없음 권한을 가진 역할에 추가된 멤버는 다른 권한이 부여될 때까지 데이터베이스를 수정하거나, 프로세스 작업을 실행하거나, 데이터를 쿼리하거나, 데이터베이스를 볼 수 없습니다.  
  
 그룹 또는 사용자 역할의 여러 다른 권한 가진 각 역할의 구성원이 수 있습니다. 사용자가 여러 역할의 멤버인 경우 각 역할에 대해 정의된 사용 권한은 누적됩니다. 예를 들어 사용자가 읽기 권한을 가진 역할의 멤버인 동시에 없음 권한을 가진 역할의 멤버일 경우 해당 사용자는 읽기 권한을 가집니다.  
  
 각 역할은 다음 중 하나의 권한을 가질 수 있습니다.  
  
|Permissions|Description|DAX를 사용하는 행 필터|  
|-----------------|-----------------|----------------------------|  
|InclusionThresholdSetting|멤버는 model 데이터베이스 스키마를 수정할 수 없으며 데이터를 쿼리할 수 없습니다.|행 필터는 적용되지 않습니다. 데이터가 이 역할의 사용자에게 표시되지 않습니다.|  
|읽기|멤버는 행 수준 필터를 기반으로 데이터를 쿼리할 수 있지만 SSMS의 model 데이터베이스를 볼 수 없으며, model 데이터베이스 스키마를 변경할 수 없고, 사용자가 모델을 처리할 수 없습니다.|행 필터를 적용할 수 있습니다. 행 필터 DAX 수식에 지정된 데이터만 사용자에게 표시됩니다.|  
|읽기 및 처리|멤버는 행 수준 필터를 기반으로 데이터를 쿼리할 수 있고 처리 명령을 포함하는 스크립트 또는 패키지를 실행하여 처리 작업을 실행할 수 있지만 데이터베이스를 변경할 수 없습니다. SSMS에서 model 데이터베이스를 볼 수 없습니다.|행 필터를 적용할 수 있습니다. 행 필터 DAX 수식에 지정된 데이터만 쿼리할 수 있습니다.|  
|처리|멤버는 처리 명령을 포함하는 스크립트 또는 패키지를 실행하여 처리 작업을 실행할 수 있습니다. model 데이터베이스 스키마를 수정할 수 없습니다. 데이터를 쿼리할 수 없습니다. SSMS에서 model 데이터베이스를 쿼리할 수 없습니다.|행 필터는 적용되지 않습니다. 이 역할에서는 데이터를 쿼리할 수 없습니다.|  
|관리자|멤버는 모델 스키마를 수정할 수 있으며 모델 디자이너, 보고 클라이언트 및 SSMS에서 모든 데이터를 쿼리할 수 있습니다.|행 필터는 적용되지 않습니다. 이 역할에서는 모든 데이터를 쿼리할 수 있습니다.|  
  
##  <a name="bkmk_rowfliters"></a> Row filters  
 행 필터는 특정 역할의 멤버가 쿼리할 수 있는 테이블의 행을 정의합니다. 행 필터는 DAX 수식을 사용하여 모델의 각 테이블에 대해 정의됩니다.  
  
 읽기 권한과 읽기 및 처리 권한을 가진 역할에 대해서만 행 필터를 정의할 수 있습니다. 기본적으로 특정 테이블에 대해 행 필터를 정의하지 않을 경우 읽기 권한 또는 읽기 및 처리 권한을 가진 역할의 멤버는 다른 테이블에서 교차 필터링이 적용되지 않는 한 테이블의 모든 행을 쿼리할 수 있습니다.  
  
 특정 테이블에 대해 행 필터를 정의할 경우 TRUE/FALSE 값으로 평가되어야 하는 DAX 수식을 통해 해당 역할의 멤버가 쿼리할 수 있는 행을 정의합니다. DAX 수식에 포함되지 않은 행은 쿼리할 수 없습니다. 예를 들어 Sales 역할 멤버에 대해서 행 필터 식, *=Customers [Country] = “USA”*를 가진 Customers 테이블에서 Sales 역할 멤버는 USA의 고객만 볼 수 있습니다.  
  
 행 필터는 지정된 행과 관련 행에 적용됩니다. 테이블에 여러 관계가 있는 경우 필터는 활성 관계에 대한 보안을 적용합니다. 행 필터는 관련 테이블에 대해 정의된 다른 행 필터와 교차됩니다. 예를 들면 다음과 같습니다.  
  
|테이블|DAX 식|  
|-----------|--------------------|  
|Region|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|트랜잭션|=Transactions[Year]=2008|  
  
 Transactions 테이블에 이러한 사용 권한이 적용되면 멤버는 고객이 USA에 있고, 제품 범주가 Bicycles이며, 연도가 2008년에 해당하는 데이터 행을 쿼리할 수 있습니다. 사용자는 해당 사용 권한이 부여된 다른 역할의 멤버가 아닌 한 미국 이외의 국가에서 발생한 거래, Bicycles 범주가 아닌 거래 또는 2008년에 발생하지 않은 거래를 쿼리할 수 없습니다.  
  
 *=FALSE()* 필터를 사용하여 전체 테이블의 모든 행에 대한 액세스를 거부할 수 있습니다.  
  
### <a name="dynamic-security"></a>동적 보안  
 동적 보안은 현재 로그온한 사용자의 사용자 이름 또는 연결 문자열에서 반환된 CustomData 속성을 기반으로 행 수준 보안을 정의하는 방법을 제공합니다. 동적 보안을 구현하려면 사용자에 대한 로그인(Windows 사용자 이름) 값이 있는 테이블과 특정 사용 권한을 정의하는 데 사용할 수 있는 필드를 모델에 포함해야 합니다(예: 로그인 ID(domain\username)가 있는 dimEmployees 테이블과 각 직원에 대한 부서 값).  
  
 동적 보안을 구현하려면 다음 기능을 DAX 수식의 일부로 사용하여 현재 로그온한 사용자의 사용자 이름 또는 연결 문자열의 CustomData 속성을 반환할 수 있습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|[USERNAME 함수(DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)|현재 로그온한 사용자의 domain\ username을 반환합니다.|  
|[CUSTOMDATA 함수(DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)|연결 문자열의 CustomData 속성을 반환합니다.|  
  
 LOOKUPVALUE 함수를 사용하여 Windows 사용자 이름이 USERNAME 함수에서 반환된 사용자 이름 또는 CustomData 함수에서 반환된 문자열과 동일한 열의 값을 반환할 수 있습니다. 그런 다음 LOOKUPVALUE에서 반환된 값이 동일한 테이블 또는 관련된 테이블의 값과 일치하는 경우로 쿼리를 제한할 수 있습니다.  
  
 예를 들어 다음 수식을 사용합니다.  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 LOOKUPVALUE 함수는 dimEmployees[LoginId]가 USERNAME에서 반환된 현재 로그온한 사용자의 LoginID와 동일하며 dimEmployees[DepartmentId]의 값이 dimDepartmentGroup[DepartmentId]의 값과 동일한 dimEmployees[DepartmentId] 열의 값을 반환합니다. LOOKUPVALUE에서 반환된 DepartmentId의 값은 dimDepartment 테이블 및 DepartmentId와 관련된 모든 테이블에서 쿼리된 행을 제한하는 데 사용됩니다. DepartmentId가 LOOKUPVALUE 함수에서 반환된 DepartmentId의 값에도 있는 행만 반환됩니다.  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|마케팅|7|  
|Bradley|David|Adventure-works\david0|마케팅|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1.|Corporate|  
|2|Executive General and Administration|  
|3|Inventory Management|  
|4|Manufacturing|  
|5|Quality Assurance|  
|6|Research and Development|  
|7|Sales and Marketing|  
  
##  <a name="bkmk_testroles"></a> Testing roles  
 모델 프로젝트를 제작할 때 Excel의 분석 기능을 사용하여 정의한 역할의 효율성을 테스트할 수 있습니다. 모델 디자이너의 **모델** 메뉴에서 **Excel에서 분석**을 클릭하면 Excel이 열리기 전에 **자격 증명 및 큐브 뷰 선택** 대화 상자가 나타납니다. 이 대화 상자에서 현재 사용자 이름, 다른 사용자 이름, 역할, 데이터 원본으로 작업 영역 모델에 연결하는 데 사용할 큐브 뷰를 지정할 수 있습니다. 자세한 내용은 참고 [Excel에서 분석](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|항목|Description|  
|-----------|-----------------|  
|[역할 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|이 항목의 태스크에서는 **역할 관리자** 대화 상자를 사용하여 역할을 만들고 관리하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Excel에서 분석](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME 함수 (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [LOOKUPVALUE 함수 (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)   
 [CUSTOMDATA 함수(DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
