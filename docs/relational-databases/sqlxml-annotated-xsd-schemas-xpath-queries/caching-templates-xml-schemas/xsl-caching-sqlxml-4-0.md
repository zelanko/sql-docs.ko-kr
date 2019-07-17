---
title: XSL 캐싱 (SQLXML 4.0) | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46c11054b4f3681a6bd0184ff77c2353b2201f57
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093229"
---
# <a name="xsl-caching-sqlxml-40"></a>XSL 캐싱(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XSL 스타일시트를 캐시하면 성능이 향상됩니다. XSL 스타일시트를 처음 캐시할 때 XSL 캐싱이 ON으로 설정되어 있으면 XSL 스타일시트가 메모리에 유지되므로 후속 처리의 성능이 향상됩니다. 기본 설정은 ON입니다.  
  
 XSL 캐시 크기를 설정하려면 레지스트리에 다음 키를 추가합니다.  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 XSL 캐시 크기는 사용 가능한 메모리와 사용 중인 XSL 스타일시트의 개수에 따라 설정해야 합니다. **XSLCacheSize** 크기의 기본값은 31입니다. XSL 액세스 속도가 느리다고 생각되면 캐시 크기를 늘리고, 메모리가 부족하면 캐시 크기를 줄일 수 있습니다.  
  
 성능을 더 높이려면 **XSLCacheSize** 를 일반적으로 사용하는 XSL 스타일시트의 개수보다 크게 설정하는 것이 좋습니다. **XSLCacheSize** 가 사용 중인 XSL 스타일시트의 개수보다 작으면 XSL 스타일시트 개수가 늘어나면서 성능이 저하됩니다. **XSLCacheSize** 는 최대 128까지 설정할 수 있습니다.  
  
 캐시된 XSL 스타일시트가 사용될 때마다 XSL 파일을 새로 고쳐야 하는지 확인하기 위해 템플릿 파일의 수정 시간이 검사됩니다. 왜냐하면 캐시 복사본보다 디스크 복사본이 최신이기 때문입니다.  
  
## <a name="see-also"></a>관련 항목  
 [서식 파일을 캐싱을 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [스키마 캐시 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
