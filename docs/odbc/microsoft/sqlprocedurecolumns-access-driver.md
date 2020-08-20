---
description: SQLProcedureColumns(Access 드라이버)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 289a4af7f329e88156e1ae3451f12aa40aeaa660
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500146"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 응용 프로그램 개발자는 결과 집합의 끝에서 시작 하 고 뒤로 진행 하 여 드라이버 정의 열을 찾아야 합니다.  
  
|열|주석|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT 또는 SQL_RESULT_COL|  
|순서로|이 열은 결과 집합의 끝에 반환 되는 드라이버 관련 열입니다. 열의 SQL 유형이 정수입니다.|
