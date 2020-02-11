---
title: 캐시 관리 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72e36e7d8f0efc9880d0dd164a253030712ee120
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727589"
---
# <a name="managing-caches-xmla"></a>캐시 관리(XMLA)
  XML for Analysis (XMLA)의 [clearcache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) 명령을 사용 하 여 지정 된 차원 또는 파티션의 캐시를 지울 수 있습니다. 캐시를 지우면 강제로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 해당 개체에 대 한 캐시를 다시 빌드합니다.  
  
## <a name="specifying-objects"></a>개체 지정  
 `ClearCache` 명령의 [개체](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 속성은 다음 개체 중 하나에 대 한 개체 참조만 포함할 수 있습니다. 따라서 다음 개체 이외의 다른 개체에 대한 개체 참조인 경우 오류가 발생합니다.  
  
 데이터베이스  
 데이터베이스 내의 모든 차원 및 파티션에 대한 캐시를 지웁니다.  
  
 차원  
 지정된 차원에 대한 캐시를 지웁니다.  
  
 Perspective  
 큐브의 측정값 그룹에 포함된 모든 파티션에 대한 캐시를 지웁니다.  
  
 측정값 그룹  
 측정값 그룹에 포함된 모든 파티션에 대한 캐시를 지웁니다.  
  
 파티션  
 지정된 파티션에 대한 캐시를 지웁니다.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
