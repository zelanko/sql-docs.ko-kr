---
title: SQLTransact (액세스 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f88d3154925ab589a8519cb9205da03e8c3dc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299269"
---
# <a name="sqltransact-access-driver"></a>SQLTransact(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 Microsoft Access 드라이버를 사용하면 **SQLTransact**에 대한 호출에서 *fType* 인수에 대해 SQL_COMMIT 및 SQL_ROLLBACK 지원됩니다.  
  
 커밋 프로세스 중에 오류가 발생하는 경우 Microsoft Access 드라이버 설정에서 데이터베이스 복구 옵션을 사용하거나 **SQLConfigDataSource** 함수에서 REPAIR_DB 키워드를 사용하여 영향을 받는 데이터베이스를 복구할 수 있습니다.
