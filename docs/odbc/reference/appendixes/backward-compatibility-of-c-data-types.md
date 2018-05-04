---
title: C 데이터 형식 중 이전 버전과 호환성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c2f14b9505b6908c4e560efda27c7e2a670e73e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="backward-compatibility-of-c-data-types"></a>C 데이터 형식 중 이전 버전과 호환성
SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT으로 대체 되었습니다 ODBC의 부호 있는 정수와 부호 없는 형식: SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG SQL_C_ULONG, 및 SQL_C_STINYINT 및 SQL_C_UTINYINT 합니다. ODBC 3 *.x* ODBC 2를 사용 해야 하는 드라이버. *x* 호출 될 때 드라이버 관리자를 통해 드라이버에 전달 하기 때문에 응용 프로그램 SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT를 지원 해야 합니다.
