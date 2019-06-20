---
title: '4단원: MDS에 공급자 데이터 저장 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 678a7d6ce075e6a1082856aa7962bb3f6eec522d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489715"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>4단원: MDS에 공급자 데이터 저장
  MDS(Master Data Services)는 마스터 데이터 관리를 위한 SQL Server 솔루션입니다. MDM(마스터 데이터 관리)은 조직에서 비트랜잭션 데이터 목록을 검색 및 정의하기 위해 수행하는 작업을 의미합니다.  
  
 모델은 Master Data Services에서 최상위 조직 수준이며 마스터 데이터의 구조를 구성합니다. MDS 구현에는 하나 이상의 모델이 포함될 수 있으며, 이러한 각 모델은 비슷한 데이터를 그룹화합니다. 일반적으로 마스터 데이터는 사용자, 장소, 사물 및 개념의 네 가지 방식 중 하나로 분류할 수 있습니다. 예를 들어 Product 모델을 만들어 제품 관련 데이터를 포함하거나 Customer 모델을 만들어 고객 관련 데이터를 포함할 수 있습니다. 자세한 내용은 [모델(Master Data Services)](https://msdn.microsoft.com/library/ee633746.aspx) 을 참조하십시오.  
  
 모델은 하나 이상의 엔터티를 포함할 수 있습니다. 각 엔터티에는 특성(열)과 멤버(행)가 있습니다. 각 행에는 마스터 데이터가 포함됩니다. 이 단원에서는 Supplier 및 State라는 두 개의 엔터티가 포함된 Suppliers라는 모델을 만듭니다. Supplier 엔터티는 다음과 같은 특성이 됩니다. 코드, 이름, Contact First Name, Contact Last Name, 전자 메일 주소, Address Line, City, 상태, Zip 및 Country에 문의 합니다. 일반적으로 특성에 대한 자세한 내용은 [특성(Master Data Services)](https://msdn.microsoft.com/library/ee633745.aspx) 을 참조하십시오. Code 및 Name 특성은 Cleansed and Matched Suppliers Excel 파일에서 SupplierID 및 Supplier Name 열에 해당합니다.  
  
 도메인 기반 특성은 다른 엔터티의 멤버로 값이 채워지는 특성입니다. 도메인 기반 특성은 사용자가 유효하지 않은 특성 값을 입력하는 것을 방지합니다. 특성 값은 다른 엔터티로 채워진 드롭다운 목록에서만 선택할 수 있습니다. 이 자습서에서 Supplier 엔터티의 State 특성은 State 엔터티의 값이 포함된 도메인 기반 특성입니다. Supplier 엔터티의 State 특성 값은 State 엔터티의 값 중 하나로만 변경할 수 있습니다. 자세한 내용은 [도메인 기반 특성](../master-data-services/domain-based-attributes-master-data-services.md) 을 참조하십시오.  
  
 MDS에서 파생 계층은 모델의 도메인 기반 특성 관계로부터 파생됩니다. 이 자습서에서는 Supplier 엔터티와 State 엔터티 사이의 파생 계층을 만듭니다. 파생 계층을 만든 후에는 마스터 데이터 관리자의 브라우저에 지역 목록이 표시됩니다. 목록에서 한 지역을 클릭하면 오른쪽 창에 해당 지역의 공급자가 표시됩니다. 이 관계를 기반으로 나중에 파생 계층을 만듭니다. 자세한 내용은 [파생 계층](../master-data-services/derived-hierarchies-master-data-services.md) 을 참조하십시오.  
  
 이전 단원에서는 DQS에서 기술 자료를 작성하고 이를 사용해서 공급자 데이터를 정리 및 일치시키고, 결과를 Cleansed and Matched Supplier Data.xls 파일에 저장했습니다. 이 단원에서는 정리 및 일치된 데이터를 MDS에 업로드합니다. DQS는 데이터(메타데이터)에 대한 지식만 포함하지만 MDS는 데이터 자체(마스터 집합)를 저장합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. DQS에는 여러 공급자에 대 한 지식이 포함 될 수 있지만 MDS에서는 회사에서 사용 되는 공급자를만 유지 관리 합니다.  
  
 이 단원에서는 다음 작업을 수행합니다.  
  
1.  **마스터 데이터 관리자 웹 애플리케이션** 을 사용해서 **MDS** 에서 **Suppliers**모델을 만듭니다.  
  
2.  Excel에서 **Cleansed and Matched Supplier Data.xls** 를 열고 **Excel용 MDS 추가 기능** 을 사용하여 **Supplier** 라는 엔터티를 만들고 데이터를 MDS에 업로드합니다.  
  
3.  **마스터 데이터 관리자**를 사용해서 MDS에 데이터가 생성되었는지 확인합니다.  
  
4.  **State** 라는 엔터티를 만들고 **State** 엔터티에 따라 **Supplier** 엔터티의 **State** 특성을 도메인 기반 특성으로 업데이트합니다. 이 작업은 모두 **Excel용 MDS 추가 기능**을 사용하여 수행합니다.  
  
5.  **마스터 데이터 관리자** 를 사용해서 도메인 기반 특성이 생성되었는지 확인하고 **State** 엔터티의 **Name** 특성에 대한 값을 업데이트합니다.  
  
6.  **Excel** 에서 **마스터 데이터 관리자**를 사용하여 업데이트한 내용을 확인합니다.  
  
7.  **마스터 데이터 관리자** 를 사용해서 **State** 엔터티의 값을 **Excel**에 로드하고, 값을 추가하고, 추가된 내용을 확인합니다.  
  
8.  **마스터 데이터 관리자** 를 사용해서 **Supplier** 엔터티와 **State**엔터티 사이의 도메인 기반 특성 관계를 사용하여 파생 계층을 만들고 사용합니다(Supplier 엔터티의 State 특성은 State 엔터티 유형임).  
  
## <a name="next-step"></a>다음 단계  
 [작업 1: 마스터 데이터 관리자를 사용 하 여 공급자 모델 만들기](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
