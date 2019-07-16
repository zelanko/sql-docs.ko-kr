---
title: 모듈 및 프롤로그 (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
author: rothja
ms.author: jroth
ms.openlocfilehash: f7a2df8ea534622c4ff4c1695c7e44a7aea7611d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946582"
---
# <a name="modules-and-prologs-xquery"></a>모듈 및 프롤로그(XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [XQuery 프롤로그](../xquery/modules-and-prologs-xquery-prolog.md) 일련의 네임 스페이스 선언입니다. 프롤로그에서 선언 네임스페이스를 사용할 때는 네임스페이스 바인딩에 대한 접두사를 지정하고 이 접두사를 쿼리 본문에서 사용할 수 있습니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [XQuery 언어 참조&#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
