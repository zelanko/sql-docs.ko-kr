---
title: Database 요소 (DTA) 서버용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 341c267b686a56a37390e0ee774df0aa20e73fd8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049823"
---
# <a name="database-element-for-server-dta"></a>Server의 Database 요소(DTA)
  특정 서버에서 튜닝할 데이터베이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|발생 빈도|당 한 번 이상 필요한 `Server` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|부모 요소|[Server 요소 &#40;DTA&#41;](server-element-dta.md)|  
|자식 요소|[데이터베이스에 대 한 요소 이름을 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [데이터베이스에 대 한 스키마 요소 &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseDetailsTypecomplexType** 입니다. 이 `Database` 요소와 `Configuration` 요소가 루트 부모인 요소를 혼동하지 마십시오. 자세한 내용은 [Configuration의 Database 요소&#40;DTA&#41;](database-element-for-configuration-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 사용 예는 `Database` 요소를 참조 하세요 [Server 요소 &#40;DTA&#41;](server-element-dta.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
