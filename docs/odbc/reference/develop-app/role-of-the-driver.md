---
title: 드라이버의 역할 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2687e1a68789566fd7b660a8241d65ff4714a933
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633571"
---
# <a name="role-of-the-driver"></a>드라이버의 역할
모든 오류 및 경고 드라이버 관리자에서 확인 하지 확인 하 고 생성 하는 상태 레코드를 정렬 하는 드라이버. (ODBC 2입니다. *x* 드라이버 상태 레코드 순서를 지정 하지 않습니다.) 이 오류 및 경고 데이터 잘림, 데이터 변환, 구문 및 상태 전환에 포함합니다. 드라이버는 오류 및 경고 드라이버 관리자에 의해 부분적으로 검사를 검사할 수 있습니다. 예를 들어 드라이버 관리자를 확인 하지만 여부를 값 *작업* 에 **SQLSetPos** 는 드라이버가 지원 되는지 여부를 확인 해야 합니다.  
  
 드라이버 매핑하여 *네이티브 오류* -데이터 원본에서 반환 하는 오류,-Sqlstate를 합니다. 예를 들어 드라이버 구문이 잘못 되었습니다 SQL sqlstate 42000 (구문 오류 또는 액세스 위반)에 대 한 다양 한 네이티브 오류 개수를 매핑할 수 있습니다. 드라이버 상태 레코드의 SQL_DIAG_NATIVE 필드에 원시 오류 번호를 반환합니다. 오류 및 경고에 매핑되는 방법을 데이터 원본의 인수에서 드라이버 설명서를 표시할지 **SQLGetDiagRec** 하 고 **SQLGetDiagField**합니다.
