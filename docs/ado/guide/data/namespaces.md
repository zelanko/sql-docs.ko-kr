---
title: "네임 스페이스 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c34bb680f7a066eeb694cf62fba39cabb0d4cbea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="namespaces"></a>네임스페이스
다음 4 개의 네임 스페이스를 사용 하는 ADO의 XML 지 속성 형식입니다.  
  
## <a name="remarks"></a>주의  
 다음 4 개의 네임 스페이스를 사용 하는 ADO의 XML 지 속성 형식입니다.  
  
|접두사|Description|  
|------------|-----------------|  
|s|요소와 현재 레코드 집합의 스키마를 정의 하는 특성이 포함 된 "XML 데이터" 네임 스페이스를 참조 합니다.|  
|dt|지정 된 데이터 형식 정의를 참조합니다.|  
|rs|요소를 포함 하는 네임 스페이스 및 ADO 레코드 집합 속성에 관련 특성 및 특성을 가리킵니다.|  
|z|현재 행 집합의 스키마를 참조 합니다.|  
  
 클라이언트는 사양에 정의 된 대로 고유 태그 이러한 네임 스페이스를 추가 하지 해야 합니다. 예를 들어 클라이언트가 정의 안와 네임 스페이스 ":-microsoft-com:rowset" 다음 "rs: MyOwnTag."와 같은 작업을 기록 네임 스페이스에 대 한 자세한 내용은 참조는 [W3C 네임 스페이스에 XML 권장 사항의](http://www.w3.org/TR/REC-xml-names/)합니다.  
  
> [!IMPORTANT]
>  스키마 태그에 대 한 ID "RowsetSchema" 해야 하며 현재 행 집합의 스키마를 참조 하는 데 사용 되는 네임 스페이스 "#RowsetSchema"을 가리켜야 합니다.  
  
 네임 스페이스의 접두사-콜론과 등호 사이의 부분 —는 임의로 지정 됩니다.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 사용자 이름일으로이 이름은 XML 문서 전체에서 일관 되 게 사용 하려면이 옵션을 정의할 수 있습니다. ADO를 항상 "s", "rs", "dt" 작성 되며 "z" 하지만 이러한 접두사 이름은 없습니다 로드 구성 요소에 하드 코딩 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
