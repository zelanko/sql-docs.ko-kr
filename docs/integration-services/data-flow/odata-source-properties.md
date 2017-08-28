---
title: "OData 원본 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 64e297a37c3b6449551968b5788f8c2c0ddd4ab6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source-properties"></a>OData 원본 속성
마우스 **OData 원본** 클릭 확인 하 고 데이터 흐름에서 **속성**, 속성에 대 한 참조는 **OData 원본** 구성 요소를 **속성** 창.  

## <a name="properties"></a>속성 
|속성|Description|  
|-|-|  
|CollectionName|OData 서비스에서 검색할 컬렉션의 이름입니다. **CollectionName** 속성은 **UseResourcePath** 가 False인 경우 사용됩니다.<br /><br /> 이 속성은 expressionable 런타임 시 값을 설정할 수 있습니다. 그러나 컬렉션의 메타 데이터 디자인 타임에 있는 메타 데이터와 일치 하지 않는 경우 유효성 검사 오류가 발생 하는 실패 하 여 데이터 흐름 실행이 발생 합니다.|  
|DefaultStringLength|이 값은 최대 길이가 없는 문자열 열의 기본 길이를 지정합니다.<br /><br /> **기본값:** 4000|  
|Query|OData 쿼리 매개 변수입니다. 이 속성은 expressionable 이며 런타임에 설정할 수 있습니다.|  
|ResourcePath|컬렉션 이름을 선택하는 대신 전체 리소스 경로를 지정해야 하는 경우 이 속성을 사용합니다. 이 속성은 **UseResourcePath** 가 True인 경우 사용됩니다.|  
|UseResourcePath|True로 설정되면 OData 피드 위치를 결정하기 위해 **ResourcePath** 값이 기본 URL에 추가됩니다. False로 설정되면 **CollectionName** 값이 사용됩니다.<br /><br /> **기본값:** False|  
  
## <a name="see-also"></a>참고 항목
[OData 원본](odata-source.md)

