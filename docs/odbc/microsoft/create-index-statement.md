---
title: CREATE INDEX 문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280973"
---
# <a name="create-index-statement"></a>CREATE INDEX 문
CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 CREATE [UNIQUE] 인덱스 *인덱스 이름* ( *테이블 이름* ) (*열 식별자* [asc] [desc] [, *열 식별자* [asc] [desc] ...]) \< *인덱스 옵션 목록* 포함>  
  
 여기서 \< *인덱스 옵션 목록*>는 기본 &#124; null 허용 안 함 &#124; null을 무시 합니다.  
  
 Microsoft Access 드라이버만 NULL 허용 안 함 및 NULL 인덱스 무시 옵션을 사용 합니다. DBASE 및 Paradox 드라이버는 구문을 적용 하지만 두 옵션의 존재는 무시 합니다.  
  
 Paradox 드라이버를 사용 하는 경우 CREATE INDEX 문은 Paradox 기본 키 파일과 보조 파일을 만듭니다.  
  
 Microsoft Excel 또는 텍스트 드라이버에서는이 문을 지원 하지 않습니다.
