---
title: 운전자의 역할 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304285"
---
# <a name="role-of-the-driver"></a>드라이버의 역할
드라이버는 드라이버 관리자가 확인하지 않은 모든 오류 및 경고를 확인하고 생성되는 상태 레코드를 주문합니다. (ODBC 2. *x* 드라이버는 상태 레코드를 주문하지 않습니다.) 여기에는 데이터 잘림, 데이터 변환, 구문 및 일부 상태 전환의 오류 및 경고가 포함됩니다. 또한 운전자는 드라이버 관리자가 부분적으로 확인한 오류 및 경고를 확인할 수도 있습니다. 예를 들어 드라이버 관리자는 **SQLSetPos에서** *작업* 값이 합법적인지 여부를 확인하지만 드라이버는 지원되는지 확인해야 합니다.  
  
 또한 드라이버는 *기본* 오류(즉, 데이터 원본에서 반환되는 오류)를 SQLSTATEs에 매핑합니다. 예를 들어 드라이버는 잘못된 SQL 구문에 대한 여러 가지 기본 오류를 SQLSTATE 42000(구문 오류 또는 액세스 위반)에 매핑할 수 있습니다. 드라이버는 상태 레코드의 SQL_DIAG_NATIVE 필드에 기본 오류 번호를 반환합니다. 드라이버 설명서에는 데이터 원본에서 **SQLGetDiagRec** 및 **SQLGetDiagField**의 인수에 오류 및 경고가 매핑되는 방법을 보여 야 합니다.
