---
title: SQL절차열(액세스 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be17776ac6b6879140a7c57bede1b3cb539d97be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299463"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 응용 프로그램 개발자는 결과 집합의 끝에서 시작하여 뒤로 진행하는 드라이버 정의 열을 찾아야 합니다.  
  
|열|주석|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 또는 SQL_RESULT_COL|  
|서|이 열은 결과 집합의 끝에 반환되는 드라이버 별 열입니다. 열의 SQL 형식은 정수입니다.|
