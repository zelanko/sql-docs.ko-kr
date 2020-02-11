---
title: 지원 되는 ODBC SQL 문법 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 535f2feaf17d2060c1c65e7aba17951bb3339a5d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080066"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>지원되는 ODBC SQL 문법(Visual FoxPro ODBC 드라이버)
Microsoft Visual FoxPro ODBC 드라이버는 다음을 지원 합니다.  
  
-   ODBC 최소 SQL 문법의 모든 SQL 문 및 절입니다.  
  
-   ODBC core SQL 문법의 추가 SQL 문  
  
 다음 표에는 ODBC SQL 문법 수준별로 드라이버에서 지 원하는 항목이 나열 되어 있습니다.  
  
|Level|요소|항목|  
|-----------|--------------|----------|  
|최소|데이터 정의 언어(DDL)|CREATE TABLE 및 DROP TABLE|  
||데이터 조작 언어(DML)|SELECT, INSERT, UPDATE 및 DELETE|  
||식|Simple (예: A>B + C)|  
||데이터 형식|CHAR, VARCHAR 또는 LONG VARCHAR|  
  
 지원 되는 ODBC SQL 문법 외에도 Visual FoxPro ODBC 드라이버는 다음 Visual FoxPro 명령에 대 한 완전 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다.  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [태그 삭제](../../odbc/microsoft/delete-tag-command.md)  
  
 [테이블 삭제](../../odbc/microsoft/drop-table-command.md)  
  
 [INDEX](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
