---
title: 네임 스페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a5f28b5d593524288a755f4c9455bba39554d7bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924812"
---
# <a name="namespaces"></a>네임스페이스
ADO의 XML 지 속성 형식은 다음 네 가지 네임 스페이스를 사용 합니다.  
  
## <a name="remarks"></a>설명  
 ADO의 XML 지 속성 형식은 다음 네 가지 네임 스페이스를 사용 합니다.  
  
|접두사|Description|  
|------------|-----------------|  
|s|현재 레코드 집합의 스키마를 정의 하는 요소와 특성을 포함 하는 "XML 데이터" 네임 스페이스를 참조 합니다.|  
|DT|데이터 형식 정의 사양을 참조 합니다.|  
|rs|ADO 레코드 집합 속성 및 특성과 관련 된 요소 및 특성을 포함 하는 네임 스페이스를 참조 합니다.|  
|z|현재 행 집합의 스키마를 참조 합니다.|  
  
 사양에 정의 된 대로 클라이언트는 이러한 네임 스페이스에 자체 태그를 추가 하면 안 됩니다. 예를 들어 클라이언트에서 네임 스페이스를 "urn: MyOwnTag: rowset"으로 정의 하지 않고 "rs:"와 같은 항목을 작성 해야 합니다. 네임 스페이스에 대 한 자세한 내용은 [XML 권장 사항에서 W3C 네임 스페이스](http://www.w3.org/TR/REC-xml-names/)를 참조 하세요.  
  
> [!IMPORTANT]
>  스키마 태그의 ID는 "RowsetSchema" 여야 하 고 현재 행 집합의 스키마를 참조 하는 데 사용 되는 네임 스페이스는 "#RowsetSchema"을 가리켜야 합니다.  
  
 네임 스페이스의 접두사 (콜론과 등호 사이에 있는 부분)는 임의의 접두사입니다.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 이 이름이 XML 문서 전체에서 일관 되 게 사용 되는 경우 사용자는이 이름을 모든 이름으로 정의할 수 있습니다. ADO는 항상 "s", "rs", "dt" 및 "z"를 작성 하지만 이러한 접두사 이름은 로드 구성 요소에 하드 코딩 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
