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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93ddc3881796aee3194ec5268afc68ecbab1a487
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782891"
---
# <a name="create-index-statement"></a>CREATE INDEX 문
CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 [UNIQUE] 인덱스 만들기 *인덱스 이름* ON *테이블 이름* (*열 식별자* [ASC] [DESC] [, *열 식별자* [ASC][DESC]...]) 사용 하 여 \< *인덱스 옵션 목록*>  
  
 여기서 \< *인덱스 옵션 목록을*> 일 수 있습니다: 기본 &#124; NULL 허용 안 함 &#124; NULL 무시  
  
 Microsoft Access 드라이버에만 NULL 허용 안 함 및 NULL 무시 인덱스 옵션을 사용 합니다. DBASE 및 Paradox 드라이버 구문을 허용 하지만 두 옵션의 존재를 무시 합니다.  
  
 Paradox 드라이버를 사용 하는 경우 CREATE INDEX 문의 Paradox 기본 키 파일 및 보조 파일을 만듭니다.  
  
 이 문은 Microsoft Excel 또는 텍스트 드라이버에서 지원 되지 않습니다.
