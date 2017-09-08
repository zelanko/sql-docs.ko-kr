---
title: "모듈 및 프롤로그 (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2253aae6b19fcede1465ba6d0cef5b479f5be8af
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="modules-and-prologs-xquery"></a>모듈 및 프롤로그(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 는 일련의 네임 스페이스 선언 합니다. 프롤로그에서 선언 네임스페이스를 사용할 때는 네임스페이스 바인딩에 대한 접두사를 지정하고 이 접두사를 쿼리 본문에서 사용할 수 있습니다.  
  
## <a name="implementation-limitations"></a>구현 시 제한 사항  
 다음 XQuery 사양은 이 구현에서 지원되지 않습니다.  
  
-   모듈 선언(`version`)  
  
-   모듈 선언(`module namespace`)  
  
-   Xmpspacedeclaration (`xmlspace`)  
  
-   기본 데이터 정렬 선언(`declare default collation`)  
  
-   기본 URI 선언(`declare base-uri`)  
  
-   구성 선언(`declare construction`)  
  
-   기본 정렬 선언(`declare ordering`)  
  
-   스키마 가져오기(`import schema namespace`)  
  
-   모듈 가져오기(`import module`)  
  
-   프롤로그의 변수 선언(`declare variable`)  
  
-   함수 선언(`declare function`)  
  
## <a name="in-this-section"></a>섹션 내용  
 [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md)  
 XQuery 프롤로그에 대해 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
