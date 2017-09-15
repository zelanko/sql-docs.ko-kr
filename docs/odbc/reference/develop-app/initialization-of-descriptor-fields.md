---
title: "설명자 필드의 초기화 | Microsoft Docs"
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
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a42ff3940f5d1620c7ee310df24016dfa39a4cd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="initialization-of-descriptor-fields"></a>설명자 필드의 초기화
응용 프로그램 행 설명자를 할당할 때 해당 필드에 표시 된 대로 초기 값을 수신 하는 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)합니다. SQL_DESC_TYPE 필드의 초기 값은 SQL_DEFAULT 합니다. 이 응용 프로그램에 표시 하기 위해 데이터베이스 데이터의 표준 처리를 제공합니다. 응용 프로그램 설명자 레코드의 필드를 설정 하 여 데이터의 서로 다른 처리를 지정할 수 있습니다.  
  
 설명자 헤더의 SQL_DESC_ARRAY_SIZE의 초기 값은 1입니다. 응용 프로그램 다중 행 인출 수 있도록이 필드는 수정할 수 있습니다.  
  
 기본값의 개념 IRD 필드에 대해 올바르지 않습니다. 연결 된 준비 또는 실행 된 문의 경우에 응용 프로그램 IRD 필드에 대 한 액세스를 얻을 수 있습니다.  
  
 IPD의 특정 필드는 IPD 드라이버에 의해 자동으로 구성 되었습니다 후에 정의 됩니다. 그렇지 않은 경우 정의 되지 않습니다. 이러한 필드는 SQL_DESC_CASE_SENSITIVE "," SQL_DESC_FIXED_PREC_SCALE "," 인 SQL_DESC_TYPE_NAME "," SQL_DESC_UNSIGNED, "및" SQL_DESC_LOCAL_TYPE_NAME 합니다.
