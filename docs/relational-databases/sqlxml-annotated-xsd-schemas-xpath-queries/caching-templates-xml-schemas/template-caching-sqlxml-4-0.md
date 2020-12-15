---
title: 템플릿 캐싱 (SQLXML)
description: SQLXML 4.0에서 템플릿 캐싱을 사용 하 여 템플릿을 실행할 때 성능을 크게 향상 시키는 방법을 알아봅니다.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b8bb4225d5c977cb516de8a17037c92e22658b4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479314"
---
# <a name="template-caching-sqlxml-40"></a>템플릿 캐싱(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  템플릿 캐싱은 성능을 크게 개선합니다. 템플릿 캐싱이 설정되어 있으면 템플릿이 처음 실행될 때 메모리에 남아 있습니다. 따라서 후속 템플릿 실행 성능이 개선됩니다.  
  
 템플릿 캐시 크기를 설정하려면 레지스트리에 다음 키를 추가합니다.  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 템플릿 크기는 사용 가능한 메모리와 사용 중인 템플릿 개수에 따라 설정해야 합니다. **Templatecachesize** 크기의 기본값은 31입니다. 템플릿 액세스 속도가 느리다고 생각되면 캐시 크기를 늘리고, 메모리가 부족하면 캐시 크기를 줄일 수 있습니다.  
  
 성능을 향상 시키려면 일반적으로 사용 하는 템플릿 수보다 많은 **Templatecachesize** 를 설정 하는 것이 좋습니다. **TemlateCacheSize** 가 템플릿 수보다 적으면 템플릿 수가 증가 하면 성능이 저하 됩니다. **Templatecachesize** 를 최대 128로 설정할 수 있습니다.  
  
 캐시된 템플릿이 사용될 때마다 템플릿을 새로 고쳐야 하는지 확인하기 위해 템플릿 파일의 수정 시간이 검사됩니다. 왜냐하면 캐시 복사본보다 디스크 복사본이 최신이기 때문입니다.  
  
> [!NOTE]  
>  템플릿 매개 변수와 명령 속성은 캐시되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [스키마 캐싱은 SQLXML 4.0 &#40;&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [&#40;SQLXML 4.0&#41;XSL 캐싱 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
