---
title: "날짜 특성 만들기(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating date attributes [Master Data Services]
- attributes [Master Data Services], creating date attributes
ms.assetid: 22a8f1a3-b4f2-4cfa-8495-7daad5ce9d12
caps.latest.revision: "13"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a993272297b82d35cd77412d3f58c709483efaba
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="create-a-date-attribute-master-data-services"></a>날짜 특성 만들기(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 사용자가 날짜를 특성 값으로 입력할 수 있게 하려면 날짜 특성을 만듭니다.  
  
> [!NOTE]  
>  이 특성을 DateTime이라고 하지만 시간 값이 지원되지 않습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   **시스템 관리** 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   해당 특성을 만들 엔터티가 있어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
### <a name="to-create-a-date-attribute"></a>날짜 특성을 만들려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지의 표에서 모델을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지에서 해당 특성을 만들려는 엔터티의 행을 선택합니다.  
  
4.  **특성**을 클릭합니다.  
  
5.  **특성 관리** 페이지에서 다음 작업 중 하나를 수행하고 **추가**를 클릭합니다.  
  
    -   리프 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **리프** 를 선택합니다.  
  
    -   통합 멤버용 특성의 경우 **멤버 형식** 목록 상자에서 **통합** 을 선택합니다.  
  
    -   컬렉션용 특성의 경우 **멤버 형식** 목록 상자에서 **컬렉션** 을 선택합니다.  
  
6.  **이름** 상자에 특성의 이름을 입력합니다. 특성 이름으로 사용하지 않아야 하는 단어의 목록을 보려면 [예약어&#40;Master Data Services&#41;](../master-data-services/reserved-words-master-data-services.md)를 참조하세요.  
  
7.  필요에 따라 표시 이름을 입력하고 **설명** 상자에 특성의 설명을 입력합니다.  
  
8.  **탐색기** 표에 표시할 특성 열의 너비를 **표시 픽셀 폭** 상자에 입력합니다.  
  
9. **특성 유형** 목록에서 **자유 형식**을 선택합니다.  
  
10. **데이터 형식** 목록에서 **DateTime**을 선택합니다.  
  
11. **입력 마스크** 목록에서 날짜 형식을 선택합니다.  
  
12. 또는 특성 그룹의 변경 내용을 추적하려면 **변경 내용 추적 설정** 을 선택합니다. 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)를 참조하세요.  
  
13. **저장**을 클릭합니다.  
  
## <a name="to-display-the-time-portion-of-a-datetime-value"></a>날짜/시간 값의 시간 부분을 표시하려면  
 사용자 인터페이스에서 날짜/시간 값의 시간 부분을 표시하도록 하려면 특성에 대한 적절한 입력 마스크를 선택해야 합니다. 이를 수행하는 Datetime 특성의 기본 제공 마스크가 없는 경우 시간을 표시할 수 있도록 하는 새 마스크를 추가할 수 있습니다. 이렇게 하려면 기본 제공 마스크가 저장되는 MDS 데이터베이스의 mdm.tblList 테이블에 행을 추가합니다. 행의 값은 다음과 같아야 합니다.  
  
|||  
|-|-|  
|ListCode|lstInputMask|  
|ListName|입력 마스크|  
|Seq|19|  
|List Option|dd/MM/yyyy hh:mm:ss tt|  
|Option ID|19|  
|IsVisible|1|  
|Group_ID|3|  
  
 mdm.tblList 표에 위 값이 있는 행을 입력하면 입력 마스크 목록 상자에서 "dd/MM/yyyy hh:mm:ss tt" 마스크를 사용할 수 있습니다. 그러면 해당 엔터티를 선택하여 MDS 탐색기에서 엔터티의 datetime 특성 열에 날짜 및 시간을 표시할 수 있습니다.  
  
 입력 마스크는 사용자 지정 .NET DateTime 형식 문자열입니다. 자세한 내용은 [사용자 지정 날짜 및 시간 형식 문자열](https://msdn.microsoft.com/en-us/library/8kb3ddd4\(v=vs.110\).aspx)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [특성&#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [특성 이름 및 데이터 형식 변경&#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)   
 [도메인 기반 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)   
 [파일 특성 만들기&#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)  
  
  
