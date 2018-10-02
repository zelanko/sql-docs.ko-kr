---
title: 도메인 기반 특성 만들기(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- domain-based attributes [Master Data Services], creating
- creating domain-based attributes [Master Data Services]
- attributes [Master Data Services], creating domain-based attributes
ms.assetid: 11c31c9f-e6cc-47b7-b76a-d691f84c93c6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 1752fd6736ef8900c22054dfa8f7ec6799d981fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685921"
---
# <a name="create-a-domain-based-attribute-master-data-services"></a>도메인 기반 특성 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 도메인 기반 특성을 만들어서 엔터티의 멤버로 특성 값을 채웁니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   특성 값의 원본으로 사용할 엔터티가 있어야 합니다. 예를 들어 Color 엔터티를 기반으로 하는 도메인 기반 특성을 만들려면 먼저 Color 엔터티를 만들어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
-   해당 특성을 만들 엔터티가 있어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
## <a name="attribute-information"></a>특성 정보  
 생성되는 각 특성에 대해 열이 7개 포함된 행이 표에 추가됩니다. 다음 표에서는 열을 설명합니다.  
  
|Column|설명|  
|------------|-----------------|  
|상태|특성 상태입니다.<br /><br /> 저장을 클릭하면 특성이 업데이트 중임을 나타내는 ![업데이트 상태 아이콘](../master-data-services/media/mds-statusicon-updating.png "업데이트 상태 아이콘") 이미지가 표시됩니다.<br /><br /> 특성을 만들거나 편집할 때 오류가 발생하면 ![오류 상태 아이콘](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘") 이미지가 표시됩니다.<br /><br /> 그렇지 않으면 상태가 정상이고 ![정상 상태 아이콘](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘")이미지가 표시됩니다.|  
|속성|특성 이름입니다.|  
|표시 이름|특성 표시 이름입니다.|  
|설명|특성 설명입니다.|  
|표시 픽셀 폭|특성 폭입니다.|  
|유형 및 속성|특성의 유형 및 데이터 형식 정보입니다.|  
|변경 내용 추적 설정|특성의 변경 내용 추적을 사용할지 여부를 지정하고 그룹 번호를 괄호 안에 표시합니다.|  
  
 특성을 클릭하면 다음 정보가 표시됩니다.  
  
-   **만든 사람**: 특성을 만든 사용자의 이름입니다.  
  
-   **날짜**: 특성을 만든 날짜와 시간입니다.  
  
-   **업데이트한 사람**: 특성을 마지막으로 업데이트한 사용자의 이름입니다.  
  
-   **날짜**: 특성을 마지막으로 업데이트한 날짜와 시간입니다.  
  
### <a name="to-create-a-domain-based-attribute"></a>도메인 기반 특성을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지에서 모델을 클릭하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성**을 클릭합니다.  
  
5.  **특성 관리** 페이지에서 다음 작업 중 하나를 수행하고 **추가**를 클릭합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  **이름** 상자에 특성의 이름을 입력합니다. 특성 이름으로 사용하지 않아야 하는 단어의 목록을 보려면 [예약어&#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)를 참조하세요.  
  
7.  필요에 따라 표시 이름을 입력하고 **설명** 상자에 설명을 입력합니다.  
  
8.  **탐색기** 표에 표시할 특성 열의 너비를 **표시 픽셀 폭** 상자에 입력합니다.  
  
9. **특성 유형** 목록에서 **도메인 기반**을 선택합니다.  
  
10. **도메인 엔터티** 목록에서 특성 값을 채우는 데 사용할 엔터티를 선택합니다. 
  
11. **리프 멤버용 도메인 기반 특성의 경우 수행 가능한 선택적 단계:** 도메인 기반 특성에 허용되는 값을 제한하는 데 사용되는 필터 부모 특성을 선택합니다.  
  
     필터 부모 특성은 동일 엔터티 내에 있는 리프 멤버에 대한 다른 도메인 기반 특성이어야 합니다. 그리고 두 특성의 도메인 엔터티 간에 부모-자식 관계를 정의하는 수준이 포함된 파생 계층이 있어야 합니다.  
  
     허용되는 값을 제한하는 방법에 대한 자세한 내용은 Master Data Services 블로그에서 [도메인 기반 특성 드롭다운 목록을 필터링하는 방법](https://blogs.msdn.microsoft.com/mds/2015/12/03/in-sql-server-2016-master-data-services-how-to-filter-domain-based-attribute-drop-down-lists/)을 참조하세요.  
  
12. **(선택 사항)** 특성 그룹의 변경 내용을 추적하려면 **Enable change tracking** 을 선택합니다. 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)를 참조하세요.  
  
13. **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [도메인 기반 특성&#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [파생 계층 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)   
 [특성 이름 및 데이터 형식 변경&#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [특성 삭제&#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)  
  
  
