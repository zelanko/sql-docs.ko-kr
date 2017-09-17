---
title: "CREATE INDEX 문 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f6e7525059640e7ffdadd79ec26a62229eabae9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-statement"></a>CREATE INDEX 문
CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 만들기 [고유] 인덱스 *인덱스 이름* ON *테이블 이름* (*열 식별자* [ASC] [DESC] [, *열 식별자* [ASC][DESC]...]) 와 \< *인덱스 옵션 목록*>  
  
 여기서 \< *인덱스 옵션 목록*> 일 수 있습니다: 기본 &#124; NULL &#124; 허용 안 함 NULL을 무시 합니다.  
  
 Microsoft Access 드라이버만 DISALLOW NULL과 NULL 무시 인덱스 옵션을 사용합니다. DBASE 및 Paradox 드라이버 구문을 허용 하지만 두 옵션의 존재를 무시 합니다.  
  
 Paradox 드라이버를 사용 하는 경우 CREATE INDEX 문은 Paradox 기본 키 파일 및 보조 파일을 만듭니다.  
  
 이 문은 Microsoft Excel 또는 텍스트 드라이버에서 지원 되지 않습니다.
