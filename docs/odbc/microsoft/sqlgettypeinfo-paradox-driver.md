---
title: SQLGetTypeInfo (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20b5776b5b0e1490ef31ff07d1876afef326db9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711491"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 (TYPE_NAME) 형식의 이름을 반환 하 여 생성 된 테이블 **SQLGetTypeInfo** 이름이 데이터 원본에서 가장 일반적으로 사용 됩니다.  
  
 SQL_ALL_EXCEPT_LIKE이 반환할 검색할 수 있는 열에 바이트에 대 한 카운터, Double, 단일 고 Long, Short 데이터 형식입니다. (LIKE 기능 ODBC 정식 변환 함수를 사용 하는 문자 값을 변환 하 여 수행할 수 있습니다 다음 비교를 수행 합니다.)
