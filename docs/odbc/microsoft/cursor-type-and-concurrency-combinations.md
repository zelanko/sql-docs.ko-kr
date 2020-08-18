---
description: 커서 형식 및 동시성 조합
title: 커서 유형 및 동시성 조합 | Microsoft Docs
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
ms.openlocfilehash: ae82825f7b5c6f670e111b859ee02ab4ab875626
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412908"
---
# <a name="cursor-type-and-concurrency-combinations"></a>커서 형식 및 동시성 조합
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 커서 유형은 사용자에 게 제공 되는 커서의 기능을 제어 합니다. 동시성 옵션은 결과 집합의 업데이트 및 잠금 동작을 제어 합니다.  
  
|커서 유형|동시성 (허용 되는 값)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup> [키 집합 커서 사용에 대 한 제한 사항을](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)참조 하세요.  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK는 SQL_AUTOCOMMIT 연결 옵션이 SQL_AUTOCOMMIT_OFF으로 설정 된 경우에만 지원 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [연결 옵션](../../odbc/microsoft/connect-options.md)
