---
title: FOR XML 보안 고려 사항 (SQLXML)
description: SQLXML 4.0에서 FOR XML AUTO 모드를 지정할 때 중요 한 보안 고려 사항에 대해 알아봅니다.
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3b6786351f99acb34eb407de10150ffc6aeabc28
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85626855"
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>FOR XML 보안 고려 사항(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  FOR XML AUTO 모드에서는 요소 이름이 테이블 이름에 매핑되고 특성 이름이 열 이름에 매핑되는 XML 계층이 생성됩니다. 이를 통해 데이터베이스 테이블과 열 정보가 표시됩니다. AUTO 모드(서버 쪽 서식)를 사용할 때는 쿼리에 테이블 별칭과 열 별칭을 지정하여 데이터베이스 정보를 숨길 수 있습니다. 이러한 별칭은 결과 XML 문서에 요소 이름과 특성 이름으로 반환됩니다.  
  
 예를 들어 다음 쿼리에서는 AUTO 모드를 지정하므로 XML 서식이 서버에서 지정됩니다.  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 다음과 같이 결과 XML 문서에서 요소 이름과 특성 이름에 별칭이 사용됩니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 NESTED 모드(클라이언트 쪽 서식)를 사용할 때는 결과 XML 문서에서 특성에 대해서만 별칭이 반환됩니다. 기본 테이블의 이름은 항상 요소 이름으로 반환됩니다. 예를 들어 다음 쿼리에서는 NESTED 모드를 지정합니다.  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 결과 XML 문서에서 기본 테이블의 이름은 요소 이름으로 반환되고 테이블 별칭은 사용되지 않습니다.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
