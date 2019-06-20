---
title: ODBC SQL 문법 (Visual FoxPro ODBC 드라이버)를 지원 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10df35f4f29de4ac3899efa0e86e48af861f1e65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633774"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>지원되는 ODBC SQL 문법(Visual FoxPro ODBC 드라이버)
Microsoft Visual FoxPro ODBC 드라이버는 다음을 지원합니다.  
  
-   모든 SQL 문 및 ODBC 최소 SQL 문법 절  
  
-   ODBC 핵심 SQL 문법에서에서 추가 SQL 문  
  
 다음 표에서 ODBC SQL 문법의 수준에 따라 드라이버에서 지 원하는 항목을 나열 합니다.  
  
|Level|요소|항목|  
|-----------|--------------|----------|  
|최소|DDL(데이터 정의 언어)|CREATE TABLE 및 DROP TABLE|  
||DML(데이터 조작 언어)|선택, 삽입, 업데이트 및 삭제|  
||식|단순 (예: A > B + C)|  
||데이터 형식|CHAR, VARCHAR, 또는 LONG VARCHAR|  
  
 Visual FoxPro ODBC 드라이버는 지원 되는 ODBC SQL 문법, 외에도 다음 Visual FoxPro 명령에 대 한 완전 한 네이티브 Visual FoxPro 언어 구문을 지원합니다.  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [태그 삭제](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
