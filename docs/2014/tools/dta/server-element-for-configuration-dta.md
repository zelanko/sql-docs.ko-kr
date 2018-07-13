---
title: Server 요소 (DTA) 구성 | Microsoft Docs
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
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21efaa212459a89622d920c0dc4adcf2f828f1bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214273"
---
# <a name="server-element-for-configuration-dta"></a>Configuration의 Server 요소(DTA)
  데이터베이스 엔진 튜닝 관리자는 가상 구성을 평가 하려는 서버에 대 한 식별 정보를 포함 (지정 된 된 `Configuration` 요소).  
  
## <a name="syntax"></a>구문  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|당 한 번씩만 필요 `Configuration` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[구성 요소 &#40;DTA&#41;](configuration-element-dta.md)|  
|**자식 요소**|[서버에 대 한 요소 이름을 &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Configuration의 database 요소 &#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 하나만 지정할 수 있습니다 `Server` 요소는 `Configuration` 요소입니다. **데이터베이스 엔진 튜닝 관리자 XML 스키마** 에서 이 요소의 이름은 [ServerTypecomplexType](http://go.microsoft.com/fwlink/?linkid=43100)입니다. 혼동 하지 마세요 `Server` 된 자식 요소는 `DTAInput` 요소입니다. 자세한 내용은 [Server 요소&#40;DTA&#41;](server-element-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 예제&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
