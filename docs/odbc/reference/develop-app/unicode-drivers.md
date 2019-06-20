---
title: 유니코드 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e555ff4a3b33c4c827371dc1ad63546736d7189
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473034"
---
# <a name="unicode-drivers"></a>유니코드 드라이버
유니코드 드라이버 또는 ANSI 드라이버를 드라이버에 해야 하는지 여부를 하는 작업은 데이터 소스의 특성에 따라 완전히 달라 집니다. 데이터 원본에서 유니코드 데이터를 지 원하는 경우 드라이버는 유니코드 드라이버 이어야 합니다. 데이터 원본에서만 ANSI 데이터를 지 원하는 경우 ANSI 드라이버를 드라이버에 유지 되어야 합니다.  
  
 유니코드 드라이버 내보내야 **SQLConnectW** 드라이버 관리자에 의해 유니코드 드라이버 인식 됩니다.  
  
 유니코드 드라이버 유니코드 함수에 동의 해야 합니다 (의 접미사로 *W*) 유니코드 데이터를 저장 하 고 있습니다. ANSI 함수를 그대로 사용할 수도 있습니다 있지만 하지 않아도 됩니다. (드라이버 관리자를 사용 하 여 ANSI 함수 호출을 통과 하지 못한 합니다 *는* 접미사 드라이버 하지만 ANSI 되도록 함수 접미사 및 다음 전달 하지 않고 호출으로 변환 합니다.이 드라이버.)  
  
 유니코드 드라이버 응용 프로그램의 바인딩을 따라 유니코드 또는 ANSI 중 하나에 결과 집합을 반환할 수 있어야 합니다. 응용 프로그램이 바인딩하 SQL_C_CHAR, 유니코드 드라이버 SQL_CHAR SQL_WCHAR 데이터 변환 해야 합니다. 드라이버 관리자가 매핑할 SQL_C_WCHAR SQL_C_CHAR ANSI 드라이버용 않지만 유니코드 드라이버에 대 한 매핑이 없습니다.  
  
> [!NOTE]  
>  드라이버 관리자를 호출 하는 드라이버 종류를 결정할 때는 **SQLSetConnectAttr** 연결 시 SQL_ATTR_ANSI_APP 특성을 설정 합니다. 응용 프로그램에서 ANSI Api를 사용 중인 경우 SQL_ATTR_ANSI_APP SQL_AA_TRUE로 설정 됩니다 하 고 유니코드를 사용 하는 경우 SQL_AA_FALSE 값으로 설정할 수 됩니다. 드라이버 응용 프로그램 유형을 기반으로 하는 다른 동작을 나타낼 수 있도록이 특성이 사용 됩니다. 특성이 응용 프로그램에서 직접 설정할 수 없습니다 및에서 지원 되지 않습니다 **SQLGetConnectAttr**합니다. ANSI 및 유니코드 응용 프로그램에 대해 동일한 동작을 수행 하는 드라이버를 하는 경우이 특성에 대 한 sql_error가 반환 됩니다. 관계 없이 SQL_SUCCESS를 반환 하는 드라이버를 하는 경우에 드라이버 관리자 연결 풀링을 사용 하는 경우 ANSI 및 유니코드 연결에 분리 됩니다.
