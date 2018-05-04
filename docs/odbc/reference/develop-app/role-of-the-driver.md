---
title: 드라이버의 역할 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e0ef812cb4c397beeb5778c4e4764b7e79f5d0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="role-of-the-driver"></a>드라이버의 역할
드라이버는 모든 오류 및 경고 드라이버 관리자에서 확인 하지 확인 하 고 생성 하는 상태 레코드의 순서입니다. (ODBC 2입니다. *x* 드라이버 상태 레코드 순서를 지정 하지 않습니다.) 이 오류 및 경고 데이터 잘림, 데이터 변환, 구문 및 일부 상태 전환에 포함합니다. 드라이버는 오류 및 경고 부분적으로 드라이버 관리자에서 확인 됨에 확인할 수 있습니다. 예를 들어 드라이버 관리자를 확인 하지만 여부의 값 *작업* 에 **SQLSetPos** 는 드라이버가 지원 되는지 여부를 확인 해야 사용할 수 있습니다.  
  
 드라이버 매핑됩니다.이 형식은 *네이티브 오류* -데이터 소스에서 반환 하는 오류,-Sqlstate를 합니다. 예를 들어 드라이버가 잘못 된 SQL 구문 SQLSTATE 42000 (구문 오류 또는 액세스 위반)에 대 한 다른 네이티브 오류의 수를 매핑할 수 있습니다. 드라이버 상태 레코드의 SQL_DIAG_NATIVE 필드에 원시 오류 번호를 반환합니다. 오류 및 경고에 매핑되는 방법을 데이터 소스에서의 인수 드라이버 설명서를 표시할지 **SQLGetDiagRec** 및 **SQLGetDiagField**합니다.
