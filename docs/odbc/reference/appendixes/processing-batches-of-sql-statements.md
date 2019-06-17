---
title: SQL 문의 일괄 처리 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c77d60ea3ef1412e66c8bf40937b45647e776e98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639561"
---
# <a name="processing-batches-of-sql-statements"></a>SQL 문의 일괄 처리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리는 SQL_ATTR_PARAMSET_SIZE 문 특성은 1 보다 큰 SQL 문을 포함 하는 SQL 문 일괄 처리를 지원 하지 않습니다. 커서 라이브러리를 SQL 문의 일괄 처리를 전송 하는 응용 프로그램에 결과가 정의 되지 않습니다.
