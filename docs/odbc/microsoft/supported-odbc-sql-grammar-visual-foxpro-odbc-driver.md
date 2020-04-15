---
title: 지원되는 ODBC SQL 문법(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f72548d0708a63f887f7d6da4d4f5988500f0eef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304086"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>지원되는 ODBC SQL 문법(Visual FoxPro ODBC 드라이버)
마이크로소프트 비주얼 폭스프로 ODBC 드라이버는 다음을 지원합니다.  
  
-   ODBC 최소 SQL 문법의 모든 SQL 문 및 절  
  
-   ODBC 코어 SQL 문법의 추가 SQL 문  
  
 다음 표에는 ODBC SQL 문법 수준에서 드라이버가 지원하는 항목이 나열되어 있습니다.  
  
|Level|요소|항목|  
|-----------|--------------|----------|  
|최소|DDL(데이터 정의 언어)|CREATE TABLE 및 DROP TABLE|  
||DML(데이터 조작 언어)|선택, 삽입, 업데이트 및 삭제|  
||표현식|단순(예:>B+C)|  
||데이터 형식|차, 바르차 또는 롱 바르차|  
  
 지원되는 ODBC SQL 문법 외에도 Visual FoxPro ODBC 드라이버는 다음 Visual FoxPro 명령에 대한 완전한 네이티브 Visual FoxPro 언어 구문을 지원합니다.  
  
 [테이블 변경](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [삭제](../../odbc/microsoft/delete-sql-command.md)  
  
 [태그 삭제](../../odbc/microsoft/delete-tag-command.md)  
  
 [드롭 테이블](../../odbc/microsoft/drop-table-command.md)  
  
 [인덱스](../../odbc/microsoft/index-command.md)  
  
 [삽입](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [업데이트](../../odbc/microsoft/update-sql-command.md)
