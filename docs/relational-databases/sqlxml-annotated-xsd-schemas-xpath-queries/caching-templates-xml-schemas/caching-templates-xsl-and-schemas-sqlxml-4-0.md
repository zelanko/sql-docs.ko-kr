---
title: 템플릿, XSL 및 스키마 캐싱 (SQLXML)
description: SQLXML 4.0에서 템플릿, XSL 및 스키마 캐싱에 대 한 정보를 봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5d5d2400f133598f4c2434763c49463e281c3360
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524429"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>템플릿, XSL 및 스키마 캐싱(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0은 성능 개선을 위해 템플릿, XSL 및 스키마 캐싱을 지원합니다.  
  
 모든 스키마, 템플릿 및 XSL 파일 (https://또는 ftp://위치의 파일 제외)이 캐시 됩니다. 캐시된 파일은 프로세스가 실행되는 동안 메모리에 유지됩니다. 프로세스가 종료되면 모든 캐시가 손실됩니다. 따라서 쿼리당 한 프로세스를 실행하는 경우 캐시의 장점을 느끼지 못할 수 있습니다.  
  
 이 섹션의 항목에서는 캐싱에 대한 자세한 내용을 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [템플릿 캐싱은 SQLXML 4.0을 &#40;&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 템플릿 캐싱을 위한 레지스트리 키에 대해 설명하고 이를 제공합니다.  
  
 [&#40;SQLXML 4.0&#41;XSL 캐싱](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 XSL 캐싱을 위한 레지스트리 키에 대해 설명하고 이를 제공합니다.  
  
 [스키마 캐싱은 SQLXML 4.0 &#40;&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 스키마 캐싱과 연관된 SQLXML 함께 설치 문제에 대해 설명하고 스키마 캐싱을 위한 레지스트리 키를 제공합니다.  
  
  
