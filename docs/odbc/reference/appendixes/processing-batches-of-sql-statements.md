---
title: SQL 문의 일괄 처리 | 마이크로 소프트 문서
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
ms.openlocfilehash: ec0e4b67d75b1ff1b14eb11682869041717a4055
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308034"
---
# <a name="processing-batches-of-sql-statements"></a>SQL 문의 일괄 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 SQL_ATTR_PARAMSET_SIZE 문 특성이 1보다 큰 SQL 문을 포함하여 SQL 문의 일괄 처리를 지원하지 않습니다. 응용 프로그램이 SQL 문 일괄 처리를 커서 라이브러리에 제출하면 결과가 정의되지 않습니다.
