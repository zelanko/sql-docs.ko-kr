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
ms.openlocfilehash: ca9b70ee6a96759e496b831f7c12dc3ee78419b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087868"
---
# <a name="unicode-drivers"></a>유니코드 드라이버
드라이버가 유니코드 드라이버 인지 아니면 ANSI 드라이버가 데이터 원본의 특성에 따라 달라 지는 지를 나타냅니다. 데이터 원본에서 유니코드 데이터를 지 원하는 경우 드라이버는 유니코드 드라이버 여야 합니다. 데이터 원본에서 ANSI 데이터만 지 원하는 경우 드라이버는 ANSI 드라이버를 유지 해야 합니다.  
  
 유니코드 드라이버는 드라이버 관리자가 유니코드 드라이버로 인식 하도록 **Sqlconnectw** 를 내보내야 합니다.  
  
 유니코드 드라이버는 유니코드 함수 ( *W*접두사 포함)를 수락 하 고 유니코드 데이터를 저장 해야 합니다. ANSI 함수를 사용할 수도 있지만에는 필요 하지 않습니다. (드라이버 관리자는 접미사를 사용 하 여 ANSI 함수 호출을 드라이버에 전달 하지 않지만 *, 접미사를* 제외 하 고 ansi 함수 호출로 변환한 다음, 드라이버에 전달 합니다.)  
  
 유니코드 드라이버는 응용 프로그램의 바인딩에 따라 유니코드 또는 ANSI로 결과 집합을 반환할 수 있어야 합니다. 응용 프로그램이 SQL_C_CHAR에 바인딩되면 유니코드 드라이버가 SQL_WCHAR 데이터를 SQL_CHAR로 변환 해야 합니다. 드라이버 관리자는 ANSI 드라이버에 대 한 SQL_C_WCHAR를 SQL_C_CHAR에 매핑되므로 유니코드 드라이버에 대 한 매핑을 수행 하지 않습니다.  
  
> [!NOTE]  
>  드라이버 유형을 결정할 때 드라이버 관리자는 **SQLSetConnectAttr** 를 호출 하 고 연결 시 SQL_ATTR_ANSI_APP 특성을 설정 합니다. 응용 프로그램에서 ANSI Api를 사용 하는 경우 SQL_ATTR_ANSI_APP SQL_AA_TRUE로 설정 되 고 유니코드를 사용 하는 경우 SQL_AA_FALSE 값으로 설정 됩니다. 이 특성은 드라이버가 응용 프로그램 유형에 따라 다른 동작을 나타낼 수 있도록 하는 데 사용 됩니다. 특성은 응용 프로그램에서 직접 설정할 수 없으며 **SQLGetConnectAttr**에서 지원 되지 않습니다. 드라이버가 ANSI 및 유니코드 응용 프로그램에 대해 동일한 동작을 발생 하는 경우이 특성에 대 한 SQL_ERROR를 반환 해야 합니다. 드라이버가 SQL_SUCCESS을 반환 하는 경우 연결 풀링이 사용 될 때 드라이버 관리자는 ANSI 및 유니코드 연결을 분리 합니다.
