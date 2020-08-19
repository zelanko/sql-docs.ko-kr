---
description: CREATE INDEX 문
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
ms.openlocfilehash: 7a3f5a13624cdb137e8c86cf2c27044c6705298f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483636"
---
# <a name="create-index-statement"></a>CREATE INDEX 문
CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 CREATE [UNIQUE] 인덱스 *인덱스 이름* ( *테이블 이름* ) (*열 식별자* [asc] [desc] [, *열 식별자* [asc] [desc] ...]) 는 \<*index option list*>  
  
 \<*index option list*>사용할 수 있는 위치: 기본 &#124; NULL 허용 안 함 &#124; null을 무시 합니다.  
  
 Microsoft Access 드라이버만 NULL 허용 안 함 및 NULL 인덱스 무시 옵션을 사용 합니다. DBASE 및 Paradox 드라이버는 구문을 적용 하지만 두 옵션의 존재는 무시 합니다.  
  
 Paradox 드라이버를 사용 하는 경우 CREATE INDEX 문은 Paradox 기본 키 파일과 보조 파일을 만듭니다.  
  
 Microsoft Excel 또는 텍스트 드라이버에서는이 문을 지원 하지 않습니다.
