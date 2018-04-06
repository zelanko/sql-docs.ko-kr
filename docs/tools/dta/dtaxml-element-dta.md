---
title: DTAXML 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4eeed88249de7d3d04bee44262d72e113a8e04ec
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="dtaxml-element-dta"></a>DTAXML 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]루트 요소의 데이터베이스 엔진 튜닝 관리자 XML 입력 또는 출력 파일 **DTAXML** 는 튜닝 입력 및 튜닝 출력을 생성 하는 데이터베이스 엔진 튜닝 관리자를 설명 하는 모든 요소를 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|Attribute|Description|  
|---------------|-----------------|  
|**xmlns:xsi**|필수 사항입니다. XML 스키마 인스턴스 네임스페이스를 식별합니다. 이 네임스페이스의 특성은 데이터베이스 엔진 튜닝 관리자 XML 파일의 유효성을 검사하는 데 사용되는 스키마를 참조하는 데 사용됩니다.<br /><br /> 필요한 값: [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|**xmlns**|필수 사항입니다. 데이터베이스 엔진 튜닝 관리자 네임스페이스를 식별합니다.<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 XML 편집기를 사용하여 데이터베이스 엔진 튜닝 관리자 XML 파일을 편집할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 가능한 참조 항목을 찾기 위해 F1 도움말과 동적 도움말에서 이 값이 사용됩니다.<br /><br /> 필요한 값:<br /><br /> [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?LinkId=43100) 네임스페이스|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|DTA XML 파일마다 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|없음|  
|**자식 요소**|[DTAInput 요소&#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)<br /><br /> **DTAOutput** 요소(자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://schemas.microsoft.com/sqlserver/) 참조)|  
  
## <a name="remarks"></a>주의  
 XML 네임스페이스에 대한 자세한 내용은 [MSDN Library의](http://go.microsoft.com/fwlink/?LinkId=7341) XML 문서의 네임스페이스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하십시오.  
  
## <a name="example"></a>예제  
 일반적인 **DTAXML** 요소의 예는 [XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조 &#40; 데이터베이스 엔진 튜닝 관리자 &#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)   
 [데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  
