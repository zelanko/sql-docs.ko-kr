---
title: "SQLProcedureColumns (Access 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1eb6158d8d70aae635b00bcd78d844f4d1443b75
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 결과 집합의 끝에서 시작 하 고 뒤로 진행 드라이버에서 정의 된 열에 대 한 응용 프로그램 개발자를 찾아야 합니다.  
  
|열|설명|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 또는 SQL_RESULT_COL|  
|서 수|이 결과 집합의 끝에 반환 되는 드라이버 관련 열입니다. 열의 SQL 형식을 정수입니다.|
