---
title: "&lt;xsd:simpleType&gt; 선언의 값 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xsd:simpleType declarations
ms.assetid: 557b972d-3af9-40bf-8382-72b05c9de1c1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6a7f0988718d6dcb5f96c52eeaa818fc4c315464
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="values-for-ltxsdsimpletypegt-declarations"></a>&lt;xsd:simpleType&gt; 선언의 값
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
다음 표에서는 인식된 모든 XSD 단순 유형 열거를 기반으로 적용되는 제한 사항에 대해 간단하게 설명합니다.  
  
 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **\<xsd:simpleType>** 선언에 NaN 값을 지원하지 않습니다. NaN 값이 포함된 스키마는 서버에서 거부됩니다.  
  
|단순 유형|제한 사항|  
|-----------------|----------------|  
|**duration**|연도 부분은 -2^31에서 2^31-1 사이여야 합니다. 월, 일, 시, 분, 초는 모두 0에서 9999 사이여야 합니다. 초 부분은 소수점 이하 셋째 자릿수까지 추가할 수 있습니다.|  
|**dateTime**|표준 시간대 하위 필드에서 시간 부분은 -14에서 +14 사이여야 합니다. 연도 부분은 1에서 9999 사이여야 합니다. 월 부분은 1에서 12 사이여야 합니다. 일 부분은 1에서 31 사이여야 하고 올바른 날짜여야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 1974-02-31과 같은 잘못된 날짜(2월에는 31일이 없음)를 검색하고 오류를 반환합니다.<br /><br /> 초 구성 요소에는 100나노초 정밀도를 사용할 수 있습니다. 표준 시간대 표시는 선택적입니다.<br /><br /> SQL Server 2005에서 지원하는 연도 범위는 -9999에서 9999까지입니다. 현재 SQL Server에서는 좀 더 제한된 연도 범위를 지원합니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.|  
|**date**|연도 부분은 1에서 9999 사이여야 합니다. 월 부분은 1에서 12 사이여야 합니다. 일 부분은 1에서 31 사이여야 하고 올바른 날짜여야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 1974-02-31과 같은 잘못된 날짜(2월에는 31일이 없음)를 검색하고 오류를 반환합니다.<br /><br /> SQL Server 2005에서 지원하는 연도 범위는 -9999에서 9999까지입니다. 현재 SQL Server에서는 좀 더 제한된 연도 범위를 지원합니다. 자세한 내용은 [형식화된 XML과 형식화되지 않은 XML 비교](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)를 참조하세요.|  
|**gYearMonth**|연도 부분은 -9999에서 9999 사이여야 합니다.|  
|**gYear**|연도 부분은 -9999에서 9999 사이여야 합니다.|  
|**gMonthDay**|월 부분은 1에서 12 사이여야 합니다. 일 부분은 1에서 31 사이여야 합니다.|  
|**gDay**|일 부분은 1에서 31 사이여야 합니다.|  
|**gMonth**|월 부분은 1에서 12 사이여야 합니다.|  
|**decimal**|이 유형의 값은 SQL 숫자 유형에 대한 형식을 따라야 합니다. 이 유형은 내부적으로 10개 자릿수가 소수 자릿수에 사용되도록 예약된 총 38개 자릿수까지의 숫자에 대한 지원을 나타냅니다.|  
|**float**|이 유형의 값은 SQL **real** 유형에 대한 형식을 따라야 합니다.|  
|**double**|이 유형의 값은 SQL **float** 유형에 대한 형식을 따라야 합니다.|  
|**string**|이 유형의 값은 SQL **nvarchar(max)** 유형에 대한 형식을 따라야 합니다.|  
|**anyURI**|이 유형의 값은 길이가 4000자(유니코드)를 초과할 수 없습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [서버의 XML 스키마 컬렉션에 대한 요구 사항 및 제한 사항](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
