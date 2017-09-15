---
title: "예약어(Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: af5326c054f80b376e43db0d18dfeb2b9ef85997
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="reserved-words-master-data-services"></a>예약어(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 모델 개체 또는 멤버를 만들 때 일부 단어를 사용할 수 없습니다. 이러한 단어를 사용하면 오류가 발생할 수 있습니다.  
  
> [!NOTE]  
>  또한 특수 문자(기호, 하이픈 등) 사용을 제한해야 합니다.  
  
-   [모델](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [엔터티](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [명시적 계층](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [특성](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [멤버](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> 모델  
 이름이 **Name** 또는 **Code**로 설정된 모델을 만드는 경우 **Name** 또는 **Code** 를 엔터티 이름으로 사용할 수 없으므로 **모델과 이름이 같은 엔터티 만들기** 를 선택하지 마십시오.  
  
##  <a name="entities"></a> 엔터티  
 엔터티 이름의 경우 **Name** 또는 **Code**를 사용할 수 없습니다.  
  
##  <a name="exhierarchies"></a> 명시적 계층  
 명시적 계층 이름의 경우 **Name** 또는 **Code**를 사용할 수 없습니다.  
  
##  <a name="attributes"></a> 특성  
  
-   **ID**  
  
-   **Code**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> 멤버  
 멤버의 경우 **코드**특성 값에 대해 **MDMMemberStatus**, **MDMUnused** 또는 **ROOT** 을 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Master Data Services 개요&#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
  
