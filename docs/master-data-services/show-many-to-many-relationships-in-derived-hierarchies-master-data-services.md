---
title: "파생된 계층 (Master Data Services)에서 다 대 다 관계 표시 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b2a9c43-40e0-48f7-a6a9-325beb9f27da
caps.latest.revision: 13
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5653a69d945fda68c197107461f6af0861135505
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="show-many-to-many-relationships-in-derived-hierarchies-master-data-services"></a>파생 계층에서 다 대 다 관계 표시(Master Data Services)
  파생 계층(DH)은 일 대 다 관계를 표시하며 다 대 다 관계도 보여줄 수 있습니다.  
  
## <a name="many-to-many-m2m-relationships"></a>다 대 다(M2M) 관계  
 두 엔터티 간의 매핑을 제공하는 세 번째 엔터티를 사용하여 두 엔터티 간의 다 대 다(M2M) 관계를 모델링할 수 있습니다.  
  
 ![mds_hierarchies_manytomany](../master-data-services/media/mds-hierarchies-manytomany.png "mds_hierarchies_manytomany")  
  
 위의 예에는 매핑 엔터티 **ClassRegistration** 으로 제공되는 **Employee** 및 **TrainingClass**엔터티 간에 M2M 관계가 있습니다. 직원은 여러 과정에 학생으로 등록될 수 있으며 각 과정은 여러 학생을 포함할 수 있습니다.  
  
 이전에는 파생 계층에서 M2M 관계를 모델링할 수 없었습니다. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]부터는 과정별 학생 등을 표시하는 파생 계층을 만들고 관계를 반전하며 과정을 학생별로 그룹화할 수 있습니다.  
  
 먼저, 파생 계층 관리 페이지로 이동하고 새 파생 계층을 만듭니다.  
  
 ![mds_hierarchies_add_derived_hierarchy](../master-data-services/media/mds-hierarchies-add-derived-hierarchy.png "mds_hierarchies_add_derived_hierarchy")  
  
 다음으로 새 파생 계층에 수준을 아래부터 위로 추가합니다. 이 예에서는 과정별로 그룹화된 학생(직원)을 보여주려고 합니다. **Employee** 엔터티는 계층에서 리프 수준이므로 먼저 추가됩니다.  
  
 ![mds_hierarchies_edit_derived_hierarchy_one](../master-data-services/media/mds-hierarchies-edit-derived-hierarchy-one.PNG "mds_hierarchies_edit_derived_hierarchy_one")  
  
 위의 스크린 샷에서는 **Employee** 엔터티가 가운데 **현재 수준** 아래 유일한 수준으로 나타납니다. 오른쪽에 있는 파생 계층 **미리 보기** 는 **Employee** 엔터티의 모든 구성원 목록을 보여 줍니다. 왼쪽에 있는 **사용 가능한 수준** 섹션은 현재 최상위 수준(**Employee**)의 맨 위에 어떤 수준을 추가할 수 있는지 보여 줍니다. 이들 중 대부분은 **Department** DBA를 포함하여 **Employee** 엔터티에서 DBA(도메인 기반 특성)입니다.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]부터는 M2M 관계를 모델링하는 새로운 유형의 수준이 있습니다(예: **Class(ClassRegistration.Student를 통해 매핑됨)**). 수준 이름은 매핑 관계를 명확하게 설명하는 데 필요한 추가 정보를 반영하기 위해 보다 세부적입니다. 이 수준을 **현재 수준** 섹션에서 **Employee** 수준으로 끌어서 놓습니다.  
  
 ![mds_hierarchies_edit_derived_hierarchy_two](../master-data-services/media/mds-hierarchies-edit-derived-hierarchy-two.PNG "mds_hierarchies_edit_derived_hierarchy_two")  
  
 이제 미리 보기에 등록된 직원이 교육 과정별로 그룹화되어 표시됩니다. M2M 관계이므로 각 자식 구성원은 여러 부모를 가질 수 있습니다. 위의 예제에서 직원 **6 {Hillman, Reinout N}** 은 **1 {Master Data Services 101}** 및 **4 {Career-Limiting Moves}**의 두 과정에 학생으로 등록됩니다.  
  
 이 매핑 관계도 반전되거나 학생별로 그룹화하여 표시될 수 있습니다.  
  
 ![mds_hierarchies_available_entities_and_hierarchies](../master-data-services/media/mds-hierarchies-available-entities-and-hierarchies.PNG "mds_hierarchies_available_entities_and_hierarchies")  
  
 다시, 자식이 둘 이상의 부모 아래 어떻게 나타날 수 있는지 확인합니다. 교육 과정 **1 {Master Data Services 101}** 이 **6 {Hillman, Reinout N}** 및 **40 {Ford, Jeffrey L}**아래에 모두 나타납니다.  
  
 매핑 엔터티 **ClassRegistration** 의 구성원은 파생 계층 내의 어느 곳에도 나타나지 않습니다. 단지 계층에서 부모 및 자식 구성원 간의 관계를 정의하는 데 사용됩니다.  
  
 다음 중 하나를 수행하고 매핑 엔터티 구성원을 수정하여 M2M 관계를 편집할 수 있습니다. M2M 관계는 **파생 계층 탐색기** 페이지에서 읽기 전용입니다.  
  
-   Excel용 MDS(Master Data Services) 추가 기능을 사용하거나 데이터 준비를 사용하여 **엔터티 탐색기** 페이지에서 매핑 엔터티 멤버를 수정합니다.  
  
-   **파생 계층 구조 탐색기**에서 자식 노드를 부모 간에 끌어서 놓습니다.  
  
     이 방법은 가능한 경우 기존 구성원을 수정하고 필요한 경우 새 구성원을 추가합니다. 기존 구성원은 삭제되지 않습니다.  
  
     예를 들어 ClassRegistration 매핑 엔터티로 학생을 사용되지 않는 노드로 이동할 때 해당 매핑 엔터티 구성원의 클래스 특성 값은 Null로 변경되며 구성원은 삭제되지 않습니다. 반대로, 학생을 사용되지 않는 노드에서 어떤 클래스로 이동할 경우 클래스가 Null인 학생에 해당하는 기존 매핑 구성원이 있으면 해당 구성원은 클래스를 Null에서 새 부모로 변경하여 수정합니다. 이러한 구성원이 없으면 추가됩니다.  
  
     이 프로세스는 구성원 삭제를 피하여 다른 사용자 데이터의 원하지 않는 삭제를 방지합니다. 예를 들어 매핑 엔터티에 부모-자식 관계를 정의하는 두 가지 이외의 다른 특성이 있는 경우가 있습니다. 사용자는 매핑 엔터티에서 직접 명시적으로 삭제를 수행해야 합니다.  
  
 새 M2M 수준은 도메인 기반 특성(DBA) 수준이 허용되는 파생 계층 내에 아무 곳에나 나타날 수 있습니다. M2M 수준은 위 예제에서와 같은 맨 위에 있을 수 있습니다. 재귀 수준을 포함하여 DBA 수준 위 및/또는 아래일 수 있습니다. 명시적 계층(사용되지 않음) 단면 수준 아래일 수 있습니다. 여러 M2M 관계를 동일한 파생 계층에서 서로 연결할 수 있습니다.  
  
 다른 파생 계층 수준과 마찬가지로 M2M 수준은 숨길 수 있습니다.  
   
### <a name="M2MSample"></a> 샘플 모델의 M2M 관계  
M2M 관계의 데모를 보려면 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에 포함된 Customer 샘플 모델의 Region Climate 파생 계층을 확인합니다.   
  
다음 그림과 같이 이 관계를 모델링하는 수준 이름은 ![mds_Number1](../master-data-services/media/mds-number1.png)**Climate(RegionClimate.Region을 통해 매핑됨)**입니다. ![mds_Number2](../master-data-services/media/mds-number2.png)**미리 보기** 에서는 지역이 연결된 기후 유형별로 그룹화되어 표시됩니다. 여러 기후(부모)와 연결된 지역(자식 멤버)이 있기 때문에 M2M 관계입니다. 예를 들어 ![mds_Number3](../master-data-services/media/mds-number3.png)**APCR {Asia Pacific}** 은 ![mds_Number4](../master-data-services/media/mds-number4.png)**A {Tropical}** 및 ![mds_Number5](../master-data-services/media/mds-number5.png)**B {Dry}**와 연결되어 있습니다.  
  
![mds_M2MRelationship_Example_CustomerModel](../master-data-services/media/mds-m2mrelationship-example-customermodel.png)  
  
Customer 샘플 모델 및 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]에 포함된 기타 샘플 모델을 배포하는 방법에 대한 지침은 [샘플 모델 및 데이터 배포](~/master-data-services/sql-server-samples-model-deployment-packages-mds.md)를 참조하세요.   
  
## <a name="one-many-relationship"></a>일 대 다 관계  
 DH의 멤버는 여러 자식 멤버의 부모일 수 있지만 일반적으로 둘 이상의 부모를 가질 수 없습니다(예외는 [멤버 보안](#bkmk_member_security)참조). 예를 들어, Employee 및 Department라는 두 개의 엔터티가 있다고 가정해보겠습니다. 여기서 각 직원은 단일 부서에 속합니다. 이 관계는 Department 엔터티를 참조하는 도메인 기반 특성(DBA)을 Employee 엔터티에 추가하여 모델링합니다.  
  
 ![mds_hierarchies_onetomany](../master-data-services/media/mds-hierarchies-onetomany.png "mds_hierarchies_onetomany")  
  
 이 경우 각 직원은 하나의 부서에만 속하지만 각 부서는 여러 직원을 가질 수 있으므로 일 대 다 관계입니다. 부서별로 그룹화된 직원을 표시하는 파생 계층을 만들 수 있습니다.  
  
 ![mds_hierarchies_dh_screenshot](../master-data-services/media/mds-hierarchies-dh-screenshot.png "mds_hierarchies_dh_screenshot")  
  
##  <a name="bkmk_member_security"></a> 멤버 보안  
 구성원 보안 권한을 할당하는 데 구성원 중복을 허용하는 계층(구성원이 둘 이상의 부모를 가질 수 있음)을 사용할 수 없습니다. 예를 들어  
  
-   null 재귀에 앵커를 지정하지 않는 재귀적 파생 계층(RDH)입니다(재귀 수준에서 각 구성원은 루트와 해당 재귀 부모 아래에 나타남).  
  
-   재귀 수준 위의 수준을 사용하는 재귀적 파생 계층입니다(재귀 수준의 각 구성원은 비재귀적 부모와 해당 재귀 부모 아래에 나타남).  
  
-   M2M 수준의 파생 계층입니다(자식이 여러 부모에 매핑될 수 있음).  
  
## <a name="collections"></a>컬렉션  
 컬렉션 및 명시적 계층은 사용되지 않습니다. 변환 저장 프로시저(udpConvertCollectionAndConsolidatedMembersToLeaf)는 컬렉션 구성원을 리프 구성원으로 변환하고 컬렉션 구성원 정보를 캡처하기 위해 다 대 다 파생 계층을 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
 [파생 계층&#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  

