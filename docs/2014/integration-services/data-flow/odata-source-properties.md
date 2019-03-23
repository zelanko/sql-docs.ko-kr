---
title: OData 원본 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fbae9e97e99223665e6d89d9e8c1a2bce3e48a26
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388841"
---
# <a name="odata-source-properties"></a>OData 원본 속성
  데이터 흐름에서 **OData 원본**을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하면 **속성** 창에 **OData 원본** 구성 요소의 속성이 표시됩니다.  
  
|||  
|-|-|  
|속성|Description|  
|CollectionName|OData 서비스에서 검색할 컬렉션의 이름입니다. **CollectionName** 속성은 **UseResourcePath** 가 False인 경우 사용됩니다.<br /><br /> 이 속성에는 식이 적용될 수 있으므로 속성 값이 런타임에 설정될 수 있습니다. 그러나 컬렉션의 메타데이터가 디자인 타임에 사용된 메타데이터와 일치하지 않는 경우 유효성 검사 오류가 발생하여 데이터 흐름 실행이 실패합니다.|  
|DefaultStringLength|이 값은 최대 길이가 없는 문자열 열의 기본 길이를 지정합니다.<br /><br /> **기본값:** 4000|  
|쿼리|OData 쿼리 매개 변수입니다. 이 속성에는 식이 적용될 수 있으므로 속성 값이 런타임에 설정될 수 있습니다.|  
|ResourcePath|컬렉션 이름을 선택하는 대신 전체 리소스 경로를 지정해야 하는 경우 이 속성을 사용합니다. 이 속성은 **UseResourcePath** 가 True인 경우 사용됩니다.|  
|UseResourcePath|True로 설정되면 OData 피드 위치를 결정하기 위해 **ResourcePath** 값이 기본 URL에 추가됩니다. False로 설정되면 **CollectionName** 값이 사용됩니다.<br /><br /> **기본값:** False|  
  
  
