---
title: 기타 주석 (SQLXML)
description: XML 대량 로드에서 각 항목을 해석 하는 방법에 대 한 설명이 포함 된 SQLXML 주석 목록을 봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fff8833c03658b5d55ba96ba27f7b1779944bd77
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479304"
---
# <a name="annotation-interpretation---other-annotations"></a>주석 해석 - 기타 주석
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XML 대량 로드는 이 섹션의 이전 항목에서 설명한 주석 외에 다음과 같은 기타 주석도 해석합니다.  
  
 **sql:id-prefix**  
 스키마에서 접두사를 XML 데이터로 지정한 경우 XML 대량 로드는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 데이터를 보내기 전에 접두사를 제거합니다.  
  
 **sql:use-cdata**  
 XML 대량 로드는 CDATA 섹션에 저장된 텍스트를 읽어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 보냅니다.  
  
 **sql:url-encode**  
 XML 대량 로드는 이 주석을 지원하지 않습니다. 예를 들어 XML 데이터 입력에 URL을 지정하면 XML 대량 로드는 데이터베이스의 해당 데이터 저장 위치에서 데이터를 읽지 못합니다.  
  
 **sql:is-mapping-schema**  
 XML 대량 로드는 이 주석이나 **sql:id** 를 지원하지 않습니다.  
  
> [!NOTE]  
>  XML 대량 로드는 인라인 매핑 스키마를 지원하지 않습니다.  
  
 **sql:key-fields**  
 XML 대량 로드는 이 주석을 항상 무시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLXML 4.0 &#40;주석 해석&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
  
  
