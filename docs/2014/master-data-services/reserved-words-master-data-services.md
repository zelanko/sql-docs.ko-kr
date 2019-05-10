---
title: 예약어(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5435c2a48417156abd6d4f831bf61c9ba6440fab
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482572"
---
# <a name="reserved-words-master-data-services"></a>예약어(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 모델 개체 또는 멤버를 만들 때 일부 단어를 사용할 수 없습니다. 이러한 단어를 사용하면 오류가 발생할 수 있습니다.  
  
> [!NOTE]  
>  또한 특수 문자(기호, 하이픈 등) 사용을 제한해야 합니다.  
  
-   [모델](#models)  
  
-   [엔터티](#entities)  
  
-   [명시적 계층](#exhierarchies)  
  
-   [특성](#attributes)  
  
-   [멤버](#members)  
  
##  <a name="models"></a> 모델  
 로 설정 된 모델을 만드는 경우 **이름을**를 선택 하지 마세요 **모델과 이름이 같은 엔터티 만들기** 때문에 **이름** 엔터티 이름에 사용할 수 없습니다.  
  
##  <a name="entities"></a> 엔터티  
 엔터티 이름의 경우 **Name** 또는 **Code**를 사용할 수 없습니다.  
  
##  <a name="exhierarchies"></a> 명시적 계층  
 명시적 계층 이름의 경우 **Name** 또는 **Code**를 사용할 수 없습니다.  
  
##  <a name="attributes"></a> 특성  
  
-   **ID**  
  
-   **코드**  
  
-   **이름**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> 멤버  
 멤버에 대해 사용할 수 없습니다 **MDMMemberStatus** 하거나 **루트** 에 대 한 합니다 **코드** 특성 값입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Master Data Services 개요](master-data-services-overview-mds.md)  
  
  
