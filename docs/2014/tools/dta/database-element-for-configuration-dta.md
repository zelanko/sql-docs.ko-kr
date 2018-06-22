---
title: Database 요소 (DTA) 구성에 대 한 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6afd8b418cd00c2ec89430e4c82613ea1af285d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081450"
---
# <a name="database-element-for-configuration-dta"></a>Configuration의 Database 요소(DTA)
  가상 구성을 평가 하려면 데이터베이스 엔진 튜닝 관리자의 대상이 될 데이터베이스를 지정 합니다 (지정 된는 `Configuration` 요소).  
  
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
|**자식 요소**|[데이터베이스에 대 한 요소 이름을 &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Database의 schema 요소 &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Recommendation 요소 &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **DatabaseTypecomplexType** 입니다. 이 `Database` 요소와 XML 입력 파일의 맨 위에서 발생하는 `Server` 요소가 루트 부모인 요소를 혼동하지 마십시오. 자세한 내용은 [Server의 Database 요소&#40;DTA&#41;](database-element-for-server-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 사용 예제를 보려면이에 대 한 `Database` 요소 참조는 [사용자 지정 구성이 포함 된 XML 입력 파일 예제 &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  