---
title: 커서 유형 및 동시성 조합 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6397b5d675546bf41102f037b68c0022bec74df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280773"
---
# <a name="cursor-type-and-concurrency-combinations"></a>커서 형식 및 동시성 조합
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 커서 유형은 사용자에게 제공되는 커서의 기능을 제어합니다. 동시성 옵션은 결과 집합의 업데이터 성 및 잠금 동작을 제어합니다.  
  
|커서 유형|동시성(허용값)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup> [키집합 기반 커서 사용의 제한 사항 참조.](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK SQL_AUTOCOMMIT 연결 옵션이 SQL_AUTOCOMMIT_OFF 설정된 경우에만 지원됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [연결 옵션](../../odbc/microsoft/connect-options.md)
