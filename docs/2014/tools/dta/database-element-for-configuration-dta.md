---
title: Database 요소 (DTA) 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fa99c86b6e4cc6705a04f0b1eecd1695033f50de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263889"
---
# <a name="database-element-for-configuration-dta"></a>Configuration의 Database 요소(DTA)
  가상 구성을 평가 하려면 데이터베이스 엔진 튜닝 관리자의 대상이 될 데이터베이스를 지정 합니다 (지정 된 된 `Configuration` 요소).  
  
## <a name="syntax"></a>구문  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|당 한 번 이상 필요한 `Server` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Configuration의 server 요소 &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**자식 요소**|[데이터베이스에 대 한 요소 이름을 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [데이터베이스에 대 한 스키마 요소 &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Recommendation 요소 &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseTypecomplexType** 입니다. 이 `Database` 요소와 XML 입력 파일의 맨 위에서 발생하는 `Server` 요소가 루트 부모인 요소를 혼동하지 마십시오. 자세한 내용은 [Server의 Database 요소&#40;DTA&#41;](database-element-for-server-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 이 사용 예 `Database` 요소를 참조 합니다 [사용자 지정 구성이 포함 된 XML 입력 파일 샘플 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
