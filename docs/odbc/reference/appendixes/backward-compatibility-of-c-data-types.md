---
title: C 데이터 형식의 이전 버전과의 호환성 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037805"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 데이터 형식의 이전 버전과의 호환성
SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT는 ODBC에서 SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG, SQL_C_STINYINT 및 SQL_C_UTINYINT로 대체 되었습니다. ODBC 2.x 응용 프로그램에서 작동 해야 하는 ODBC *2.x 드라이버는* SQL_C_SHORT, SQL_C_LONG 및 SQL_C_TINYINT를 지원 해야 *합니다 .이* 드라이버는 호출 될 때 드라이버 관리자가 드라이버에 전달 하기 때문입니다.
