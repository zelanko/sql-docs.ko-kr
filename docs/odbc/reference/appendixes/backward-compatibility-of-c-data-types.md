---
title: C 데이터 유형의 이전 버전과의 호환성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a89b282a2229b6f34833b4371081661ea51b231
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304588"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 데이터 형식의 이전 버전과의 호환성
SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT ODBC에서 SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG 및 SQL_C_ULONG, SQL_C_STINYINT 및 SQL_C_UTINYINT 서명된 형식과 서명되지 않은 유형으로 대체되었습니다. ODBC *2.x* 응용 프로그램과 함께 작동해야 하는 ODBC *3.x* 드라이버는 호출될 때 드라이버 관리자가 드라이버로 전달하기 때문에 SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT 지원해야 합니다.
