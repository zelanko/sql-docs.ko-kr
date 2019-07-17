---
title: 스키마 캐시 (SQLXML 4.0) | Microsoft 문서
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
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4ac7ee9c119daa4f1aa41c1485aae57ee280c5f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093295"
---
# <a name="schema-caching-sqlxml-40"></a>스키마 캐싱(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Microsoft SQL Server 2000 웹 릴리스 1, Microsoft SQLXML 2.0 및 SQLXML 3.0에 대 한 xml에서 병렬 설치를 모든 버전에서 다음 레지스트리 키를 사용 하 여 캐시 스키마를 명시적으로 제어할 수 있습니다.  
  
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
  
 병렬 설치에 대 한 자세한 내용은 참조 [SQLXML 4.0 s p 1의 새로운](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 스키마 캐싱은 XPath 쿼리의 성능을 크게 개선합니다. 매핑 스키마에 대해 XPath 쿼리를 실행하면 스키마가 메모리에 저장되고 필요한 데이터 구조가 메모리에 구성됩니다. 스키마 캐싱이 설정되면 스키마가 메모리에 유지되므로 후속 XPath 쿼리의 성능이 개선됩니다.  
  
 스키마 캐시 크기를 설정하려면 레지스트리에 위의 키를 추가합니다.  
  
 스키마 크기는 사용 가능한 메모리와 사용 중인 스키마 개수에 따라 설정합니다. 기본 **SchemaCacheSize** 크기는 31. 설정한 경우 **SchemaCacheSize** 높을수록 더 많은 메모리가 사용 됩니다. 따라서 스키마 액세스 속도가 느리면 캐시 크기를 늘리고 메모리가 부족하면 캐시 크기를 줄일 수 있습니다.  
  
 성능상의 이유로 좋습니다 설정 하는 **SchemaCacheSize** 일반적으로 사용 하는 매핑 스키마의 수보다 더 높은. 스키마 수가 증가 하는 경우 **SchemaCacheSize** 작은 있는 스키마의 수보다 성능이 저하 됩니다.  
  
> [!NOTE]  
>  스키마를 변경하더라도 2분 여 동안은 캐시에 반영되지 않으므로 개발 중에는 스키마를 캐싱하지 않는 것이 좋습니다.  
  
## <a name="see-also"></a>관련 항목  
 [서식 파일을 캐싱을 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [XSL 캐시 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
