---
title: SQLGetTypeInfo (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1c38b66e9b8a3c1cbed4a3712f7af866935089
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63210223"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 (TYPE_NAME) 형식의 이름을 반환 하 여 생성 된 테이블 **SQLGetTypeInfo** 이름이 데이터 원본에서 가장 일반적으로 사용 됩니다.  
  
 SQL_ALL_EXCEPT_LIKE이 반환할 검색할 수 있는 열에 바이트에 대 한 카운터, Double, 단일 고 Long, Short 데이터 형식입니다. (다음 비교를 수행 하는 ODBC 정식 변환 함수를 사용 하 여 문자 값을 변환 하 여 LIKE 기능을 구현할 수 있습니다.)  
  
 텍스트 드라이버를 사용 하면 **SQLGetTypeInfo** 데이터 형식 (CHAR 및 LONGCHAR) 텍스트 CASE_SENSITIVE FALSE 값을 반환 데이터 형식이 실제로 때 대/소문자 구분 합니다.
