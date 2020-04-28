---
title: 링크 특성 만들기
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], creating link attributes
- creating link attributes [Master Data Services]
ms.assetid: e6658e9c-5b08-4b8d-b556-17ec2dd041d2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 929e363228b30889e163519786d802dd4caee049
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728490"
---
# <a name="create-a-link-attribute-master-data-services"></a>링크 특성 만들기(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 사용자가 `https://www.contoso.com` 같은 하이퍼링크를 특성 값으로 입력할 수 있도록 하려면 링크 특성을 만듭니다.  
  
> [!NOTE]  
>  사용자가 링크 특성 값을 입력할 때 문자열은 **https://** 로 시작해야 하며, 그렇지 않으면 오류가 표시됩니다.  
  
## <a name="prerequisites"></a>전제 조건  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자 &#40;MDS(Master Data Services)&#41;](../master-data-services/administrators-master-data-services.md)를 참조 하세요.  
  
-   해당 특성을 만들 엔터티가 있어야 합니다. 자세한 내용은 [&#41;MDS(Master Data Services) 엔터티 &#40;만들기 ](../master-data-services/create-an-entity-master-data-services.md)를 참조 하세요.  
  
## <a name="attribute-information"></a>특성 정보  
 생성되는 각 특성에 대해 열이 7개 포함된 행이 표에 추가됩니다. 다음 표에서는 열을 설명합니다.  
  
|열|Description|  
|------------|-----------------|  
|상태|특성 상태입니다.<br /><br /> 저장을 클릭 하면 특성이 업데이트 되 고 있음을 나타내는 ![상태 업데이트 이미지 아이콘이](../master-data-services/media/mds-statusicon-updating.png "상태 업데이트 아이콘") 표시 됩니다.<br /><br /> 특성을 만들거나 편집할 때 오류가 발생 하면 ![오류 상태 이미지 아이콘이](../master-data-services/media/mds-statusicon-error.png "오류 상태 아이콘") 표시 됩니다.<br /><br /> 그렇지 않으면 상태가 정상 이며 ![ok 상태 이미지 아이콘이](../master-data-services/media/mds-statusicon-ok.png "정상 상태 아이콘") 표시 됩니다.|  
|Name|특성 이름입니다.|  
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
  
### <a name="to-create-a-link-attribute"></a>링크 특성을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택 하 고 **엔터티**를 클릭 합니다.  
  
3.  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성**을 클릭합니다.  
  
5.  **특성 관리** 페이지에서 다음 작업 중 하나를 수행하고 **추가**를 클릭합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  **이름** 상자에 특성의 이름을 입력합니다. 특성 이름으로 사용 하지 않아야 하는 단어의 목록을 보려면 [예약어 &#40;MDS(Master Data Services)&#41;](../master-data-services/reserved-words-master-data-services.md)를 참조 하세요.  
  
7.  필요에 따라 표시 이름을 입력하고 **설명** 상자에 특성의 설명을 입력합니다.  
  
8.  **탐색기** 표에 표시할 특성 열의 너비를 **표시 픽셀 폭** 상자에 입력합니다.  
  
9. **특성 유형** 목록에서 **자유 형식**을 선택합니다.  
  
10. **데이터 형식** 목록에서 **링크**를 선택합니다.  
  
11. **길이** 상자에 허용되는 최대 문자 수를 입력합니다.  
  
12. 또는 특성 그룹의 변경 내용을 추적하려면 **변경 내용 추적 설정** 을 선택합니다. 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)를 참조하세요.  
  
13. **저장**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [특성 &#40;MDS(Master Data Services)&#41;](../master-data-services/attributes-master-data-services.md)   
 [특성 이름 및 데이터 형식 &#40;MDS(Master Data Services)을 변경&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [도메인 기반 특성 &#40;MDS(Master Data Services)를 만듭니다&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [파일 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
