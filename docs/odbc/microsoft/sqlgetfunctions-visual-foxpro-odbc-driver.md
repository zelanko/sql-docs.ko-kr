---
title: SQLGetFunctions (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8102932a-88b3-49d8-bf7a-c766f54878c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0ae7b8eb0468dd401009ef58c83b87606b0679a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47628611"
---
# <a name="sqlgetfunctions-visual-foxpro-odbc-driver"></a>SQLGetFunctions(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 규칙:  
  
 모든 지원 되는 함수에 대해 TRUE를 반환.  
  
 Visual FoxPro ODBC 드라이버는 모든 ODBC API 핵심 및 수준 1 함수를 지원합니다. 다음 표는 드라이버 특정 수준 2 함수를 지원 하는지 여부를 나타냅니다.  
  
|*함수*|지원됨|  
|----------------|---------------|  
|SQL_API_SQLBROWSECONNECT|아니요|  
|SQL_API_SQLCOLUMNPRIVELEGES|아니요|  
|SQL_API_SQLDATASOURCES|사용자 계정 컨트롤|  
|SQL_API_SQLDESCRIBEPARAM|아니요|  
|SQL_API_SQLDRIVERS|사용자 계정 컨트롤|  
|SQL_API_SQLEXTENDEDFETCH|사용자 계정 컨트롤|  
|SQL_API_SQLFOREIGNKEYS|아니요|  
|SQL_API_SQLMORERESULTS|사용자 계정 컨트롤|  
|SQL_API_SQLNATIVESQL|아니요|  
|SQL_API_SQLNUMPARAMS|사용자 계정 컨트롤|  
|SQL_API_SQLPARAMOPTIONS|사용자 계정 컨트롤|  
|SQL_API_SQLPRIMARYKEYS|사용자 계정 컨트롤|  
|SQL_API_SQLPROCEDURECOLUMNS|아니요|  
|SQL_API_SQLPROCEDURES|아니요|  
|SQL_API_SQLSETPOS|사용자 계정 컨트롤|  
|SQL_API_SQLSETSCROLLOPTIONS|사용자 계정 컨트롤|  
|SQL_API_SQLTABLEPRIVILEGES|아니요|  
  
 자세한 내용은 [SQLGetFunctions](../../odbc/reference/syntax/sqlgetfunctions-function.md) 에 *ODBC 프로그래머 참조*합니다.
