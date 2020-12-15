---
title: 스키마 캐싱 (SQLXML)
description: 레지스트리 키를 사용 하 여 스키마 캐싱을 명시적으로 제어 하 고 SQLXML 4.0에서 XPath 쿼리의 성능을 개선 하는 방법에 대해 알아봅니다.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e92d3e4f6e22650f702c4076b014441e49bcb38
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479264"
---
# <a name="schema-caching-sqlxml-40"></a>스키마 캐싱(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Microsoft SQL Server 2000용 XML 웹 릴리스 1, Microsoft SQLXML 2.0 및 SQLXML 3.0을 함께 설치한 경우 다음 레지스트리 키를 사용하여 모든 버전에서 스키마 캐싱을 명시적으로 제어할 수 있습니다.  
  
 웹 릴리스 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 함께 설치 하는 방법에 대 한 자세한 내용은 [SQLXML 4.0 s p 1의 새로운 기능](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)을 참조 하세요.  
  
 스키마 캐싱은 XPath 쿼리의 성능을 크게 개선합니다. 매핑 스키마에 대해 XPath 쿼리를 실행하면 스키마가 메모리에 저장되고 필요한 데이터 구조가 메모리에 구성됩니다. 스키마 캐싱이 설정되면 스키마가 메모리에 유지되므로 후속 XPath 쿼리의 성능이 개선됩니다.  
  
 스키마 캐시 크기를 설정하려면 레지스트리에 위의 키를 추가합니다.  
  
 스키마 크기는 사용 가능한 메모리와 사용 중인 스키마 개수에 따라 설정합니다. 기본 **SchemaCacheSize** 크기는 31입니다. **SchemaCacheSize** 를 높게 설정 하면 더 많은 메모리가 사용 됩니다. 따라서 스키마 액세스 속도가 느리면 캐시 크기를 늘리고 메모리가 부족하면 캐시 크기를 줄일 수 있습니다.  
  
 성능상의 이유로, 일반적으로 사용 하는 매핑 스키마 수보다 **SchemaCacheSize** 을 높게 설정 하는 것이 좋습니다. 스키마 수가 늘어나면 **SchemaCacheSize** 가 보유 한 스키마 수보다 적으면 성능이 저하 됩니다.  
  
> [!NOTE]  
>  스키마를 변경하더라도 2분 여 동안은 캐시에 반영되지 않으므로 개발 중에는 스키마를 캐싱하지 않는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
 [템플릿 캐싱은 SQLXML 4.0을 &#40;&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [&#40;SQLXML 4.0&#41;XSL 캐싱 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
