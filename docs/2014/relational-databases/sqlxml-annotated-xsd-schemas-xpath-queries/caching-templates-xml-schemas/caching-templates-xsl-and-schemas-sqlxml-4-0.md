---
title: 템플릿, XSL 및 스키마 (SQLXML 4.0) 캐싱 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 279e26691ab40104bc4e77a871110b0710fb2a4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198873"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>템플릿, XSL 및 스키마 캐싱(SQLXML 4.0)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0은 성능 개선을 위해 템플릿, XSL 및 스키마 캐싱을 지원합니다.  
  
 모든 스키마, 템플릿 및 XSL 파일(http:// 또는 ftp:// 위치의 파일 제외)이 캐시됩니다. 캐시된 파일은 프로세스가 실행되는 동안 메모리에 유지됩니다. 프로세스가 종료되면 모든 캐시가 손실됩니다. 따라서 쿼리당 한 프로세스를 실행하는 경우 캐시의 장점을 느끼지 못할 수 있습니다.  
  
 이 섹션의 항목에서는 캐싱에 대한 자세한 내용을 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [템플릿 캐싱은 &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)  
 템플릿 캐싱을 위한 레지스트리 키에 대해 설명하고 이를 제공합니다.  
  
 [XSL 캐싱 &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
 XSL 캐싱을 위한 레지스트리 키에 대해 설명하고 이를 제공합니다.  
  
 [스키마 캐싱 &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
 스키마 캐싱과 연관된 SQLXML 함께 설치 문제에 대해 설명하고 스키마 캐싱을 위한 레지스트리 키를 제공합니다.  
  
  
