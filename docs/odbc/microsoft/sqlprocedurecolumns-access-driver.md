---
title: SQLProcedureColumns (Access 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1a33d449396b5cc80e8d29767708d2f9f16736fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987841"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 응용 프로그램 개발자는 결과 집합의 끝에서 시작 하 고 뒤로 진행 하 여 드라이버 정의 열을 찾아야 합니다.  
  
|열|주석|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 또는 SQL_RESULT_COL|  
|순서로|이 열은 결과 집합의 끝에 반환 되는 드라이버 관련 열입니다. 열의 SQL 유형이 정수입니다.|
