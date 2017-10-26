---
title: "SQL_NO_DATA를 반환 합니다. | Microsoft Docs"
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
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5539f9d2951913163ac6011695709e3664d8acb1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="returning-sqlnodata"></a>SQL_NO_DATA를 반환합니다.
경우는 ODBC 2. *x* 응용 프로그램 사용 ODBC 3*.x* 드라이버 호출 **SQLExecDirect**, **SQLExecute**, 또는 **SQLParamData**, 검색 된 update 또는 delete 문이 실행 된 하지만 ODBC 3 데이터 소스의 모든 행에 영항을 미치지 않았습니다 고*.x* 드라이버는 SQL_SUCCESS를 반환 해야 합니다. ODBC 3 때*.x* ODBC 3을 사용 하는 응용 프로그램*.x* 드라이버 호출 **SQLExecDirect**, **SQLExecute**, 또는 ** SQLParamData** 와 동일한 결과 ODBC 3*.x* 드라이버는 SQL_NO_DATA를 반환 해야 합니다.  
  
 검색 결과 업데이트 또는 삭제에 문이 일괄 처리 문의 영향을 주지 않습니다 데이터 소스의 모든 행 **SQLMoreResults** 관계 없이 SQL_SUCCESS를 반환 합니다. 하지 있습니다 한 결과로 생성 되는 검색 결과 업데이트/삭제 행이 없는 영향을 주는에서 더 이상 결과가 없는 이므로 SQL_NO_DATA를 반환할 수 없습니다.

