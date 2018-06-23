---
title: 예약어(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3307fb8185abfb6b862e72691596e4385b09dcb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186336"
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
 이름으로 설정 된 모델을 만드는 경우 **이름**, 선택 하지 않으면 **모델과 이름이 같은 엔터티 만들기** 때문에 **이름** 엔터티 이름에 사용할 수 없습니다.  
  
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
 멤버를 사용할 수 없습니다 **MDMMemberStatus** 또는 **루트** 에 대 한는 **코드** 특성 값입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Master Data Services 개요](master-data-services-overview-mds.md)  
  
  