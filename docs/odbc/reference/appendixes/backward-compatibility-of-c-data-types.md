---
title: C 데이터 형식의 이전 버전과 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcfc4dd2ef1bee2783f073fbb85c0d911f84305a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037805"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 데이터 형식의 이전 버전과의 호환성
SQL_C_SHORT를 SQL_C_LONG, SQL_C_TINYINT 바뀌었습니다 ODBC의 부호 있는 형식과 부호 없는 형식: SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG SQL_C_ULONG, 및 SQL_C_STINYINT 및 SQL_C_UTINYINT 합니다. ODBC *3.x* ODBC를 사용 하 여 작동 해야 하는 드라이버 *2.x* 를 호출할 때 드라이버 관리자를 통해로 전달 하기 때문에 응용 프로그램 SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT을를 지원 해야 합니다 드라이버입니다.
