---
title: "C 데이터 형식 중 이전 버전과 호환성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24d0c05a7410a3db37718ebaa667abbb01072796
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="backward-compatibility-of-c-data-types"></a>C 데이터 형식 중 이전 버전과 호환성
SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT으로 대체 되었습니다 ODBC의 부호 있는 정수와 부호 없는 형식: SQL_C_SSHORT 및 SQL_C_USHORT, SQL_C_SLONG SQL_C_ULONG, 및 SQL_C_STINYINT 및 SQL_C_UTINYINT 합니다. ODBC 3*.x* ODBC 2를 사용 해야 하는 드라이버.* x* 호출 될 때 드라이버 관리자를 통해 드라이버에 전달 하기 때문에 응용 프로그램 SQL_C_SHORT, SQL_C_LONG, 및 SQL_C_TINYINT를 지원 해야 합니다.
