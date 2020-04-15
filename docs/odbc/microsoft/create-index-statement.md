---
title: 인덱스 문 만들기 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280973"
---
# <a name="create-index-statement"></a>CREATE INDEX 문
CREATE INDEX 문의 구문은 다음과 같은 것입니다.  
  
 *테이블 이름에* [고유] 인덱스 *이름* 만들기(열*식별자* [ASC][DESC][, 열 식별자[ASC][DESC]...]) *column-identifier* 포함 \< *인덱스 옵션 목록*>  
  
 \< *인덱스 옵션 목록*> 될 수 있는 위치: 기본 &#124; NULL 을 무시 &#124; NULL을 허용하지 &#124;.  
  
 Microsoft Access 드라이버만 NULL 허용 안 및 NULL 인덱스 무시 옵션을 사용합니다. dBASE 및 역설 드라이버는 구문을 수락하지만 두 옵션 중 하나의 존재를 무시합니다.  
  
 역설 드라이버를 사용 하는 경우 CREATE INDEX 문은 역설 기본 키 파일 및 보조 파일을 만듭니다.  
  
 이 문은 Microsoft Excel 또는 텍스트 드라이버에서 지원되지 않습니다.
