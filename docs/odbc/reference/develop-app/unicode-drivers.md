---
title: "유니코드 드라이버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 195dc99394d8708e4895fce746ca13bbf724782c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="unicode-drivers"></a>유니코드 드라이버
유니코드 드라이버 또는 ANSI 드라이버는 드라이버 수 있는지 여부를 전적으로의 데이터 소스 특성에 따라 달라 집니다. 데이터 소스에서 유니코드 데이터를 지 원하는 경우 드라이버는 유니코드 드라이버 여야 합니다. 데이터 원본에서만 ANSI 데이터를 지 원하는 경우 드라이버는 ANSI 드라이버를 유지 해야 합니다.  
  
 유니코드 드라이버 내보내야 **SQLConnectW** 드라이버 관리자에서 유니코드 드라이버로 인식 되도록 합니다.  
  
 유니코드 드라이버 유니코드 함수에 동의 해야 (의 접미사와 함께 *W*) 유니코드 데이터를 저장 하 고 있습니다. 해당 ANSI 함수를 적용할 수도 있지만 데 필요 하지 않습니다. (드라이버 관리자는 ANSI 함수 호출을 전달 하지 않습니다는 *A* 접미사 ANSI에 함수 접미사와 다음 전달 하지 않고 호출으로 변환 하지만 드라이버를이 드라이버에 있습니다.)  
  
 유니코드 드라이버 ANSI 또는 유니코드 응용 프로그램의 바인딩을 따라 결과 집합을 반환할 수 있어야 합니다. 응용 프로그램 SQL_C_CHAR를 바인딩할 경우 유니코드 드라이버 SQL_CHAR SQL_WCHAR 데이터 변환 해야 합니다. 드라이버 관리자 SQL_C_WCHAR SQL_C_CHAR를 ANSI 드라이버에 대 한 매핑하지만 유니코드 드라이버에 대 한 매핑되지 않습니다.  
  
> [!NOTE]  
>  드라이버 관리자를 호출 합니다 결정할 때 드라이버 유형, **SQLSetConnectAttr** 연결 시 SQL_ATTR_ANSI_APP 특성을 설정 합니다. ANSI Api를 사용 하는 응용 프로그램 SQL_ATTR_ANSI_APP SQL_AA_TRUE, 설정 됩니다 및 SQL_AA_FALSE의 값으로 설정할 수는 유니코드를 사용 합니다. 이 특성은 드라이버 응용 프로그램 형식을 기반으로 하는 다른 동작을 나타낼 수 있도록 사용 됩니다. 특성 응용 프로그램을 직접 설정할 수 없습니다 및에서 지원 하지 않는 **SQLGetConnectAttr**합니다. 드라이버에서는 ANSI 및 유니코드 응용 프로그램에 대해 동일한 동작을 하는 경우이 특성에 대 한 SQL_ERROR를 반환 해야 합니다. 관계 없이 SQL_SUCCESS를 반환 하는 드라이버, 드라이버 관리자는 연결 풀링을 사용 하는 경우 ANSI 및 유니코드 연결을 구분 합니다.
