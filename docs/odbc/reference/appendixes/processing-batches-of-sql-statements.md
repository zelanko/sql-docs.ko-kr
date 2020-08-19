---
description: SQL 문의 일괄 처리
title: SQL 문의 일괄 처리 Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], batches
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], batches
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- SQL statements [ODBC], batches
- batches [ODBC], processing batches of SQL statements
ms.assetid: 04b93ef9-11de-47a3-8bd8-ba963c42f182
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f00d728f8a8b716d27834f82b770d25d8333a56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483216"
---
# <a name="processing-batches-of-sql-statements"></a>SQL 문의 일괄 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 SQL_ATTR_PARAMSET_SIZE statement 특성이 1 보다 큰 SQL 문을 포함 하 여 SQL 문의 일괄 처리를 지원 하지 않습니다. 응용 프로그램이 SQL 문 일괄 처리를 커서 라이브러리로 전송 하면 결과가 정의 되지 않습니다.
