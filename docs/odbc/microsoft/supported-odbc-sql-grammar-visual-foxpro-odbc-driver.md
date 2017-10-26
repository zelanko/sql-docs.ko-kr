---
title: "ODBC SQL 문법을 (Visual FoxPro ODBC 드라이버)를 지원 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: acaf0c210d31cc17e597e9e24245cc46859f44f1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>지원 되는 ODBC SQL 문법 (Visual FoxPro ODBC 드라이버)
Microsoft Visual FoxPro ODBC 드라이버가 다음을 지원합니다.  
  
-   모든 SQL 문 및 ODBC 최소 SQL 문법 절  
  
-   ODBC 핵심 SQL 문법 쿼리에서 SQL 문을 추가  
  
 다음 표에서 ODBC SQL 문법을 수준에 따라 드라이버에서 지 원하는 항목을 나열 합니다.  
  
|Level|요소|항목|  
|-----------|--------------|----------|  
|최소|DDL(데이터 정의 언어)|CREATE TABLE 및 DROP TABLE|  
||DML(데이터 조작 언어)|선택, 삽입, 업데이트 및 삭제|  
||식|단순 (예: A > B + C)|  
||데이터 형식|CHAR, VARCHAR, 또는 LONG VARCHAR|  
  
 Visual FoxPro ODBC 드라이버는 지원 되는 ODBC SQL 문법을 외에도 다음 Visual FoxPro 명령에 대 한 완전 한 네이티브 Visual FoxPro 언어 구문을 지원:  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [태그 삭제](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)

