---
title: "SQL 문의 일괄 처리 | Microsoft Docs"
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
- ODBC cursor library [ODBC], batches
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], batches
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- SQL statements [ODBC], batches
- batches [ODBC], processing batches of SQL statements
ms.assetid: 04b93ef9-11de-47a3-8bd8-ba963c42f182
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1513b2c9576d994ea7eb505c4928fd609e9498c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="processing-batches-of-sql-statements"></a>SQL 문의 일괄 처리
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 SQL_ATTR_PARAMSET_SIZE 문 특성은 1 보다 큰 SQL 문을 포함 하는 SQL 문 일괄 처리를 지원 하지 않습니다. 커서 라이브러리를 SQL 문의 일괄 처리를 전송 하는 응용 프로그램, 결과 정의 되지 않습니다.
