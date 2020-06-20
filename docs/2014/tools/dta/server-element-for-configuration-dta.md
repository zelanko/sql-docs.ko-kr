---
title: Configuration의 Server 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1d569373f80a2f5488e8612cc30da264d283cd7f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007647"
---
# <a name="server-element-for-configuration-dta"></a>Configuration의 Server 요소(DTA)
  데이터베이스 엔진 튜닝 관리자가 가상 구성(`Configuration` 요소에 의해 지정됨)을 평가하는 서버에 대한 식별 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|각 `Configuration` 요소 당 한 번씩만 필요합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Configuration 요소&#40;DTA&#41;](configuration-element-dta.md)|  
|**자식 요소**|[Server의 Name 요소&#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Configuration의 Database 요소&#40;DTA&#41;](database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>설명  
 `Server`요소에 대해 요소를 하나만 지정할 수 있습니다 `Configuration` . **데이터베이스 엔진 튜닝 관리자 XML 스키마** 에서 이 요소의 이름은 [ServerTypecomplexType](https://go.microsoft.com/fwlink/?linkid=43100)입니다. 이 `Server` 요소와 `DTAInput` 요소의 자식 요소를 혼동하지 마십시오. 자세한 내용은 [Server 요소&#40;DTA&#41;](server-element-dta.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 예제&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
