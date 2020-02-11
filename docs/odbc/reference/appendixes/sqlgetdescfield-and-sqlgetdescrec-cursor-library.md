---
title: SQLGetDescField 및 SQLGetDescRec (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 853a364b61b63d58da93111c75db0d7d723ee49b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68073910"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 및 SQLGetDescRec(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetDescField** 및 **SQLGetDescRec** 함수를 사용 하는 방법에 대해 설명 합니다. 이러한 함수에 대 한 일반적인 정보는 [SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 및 [SQLGetDescRec 함수](../../../odbc/reference/syntax/sqlgetdescrec-function.md)를 참조 하세요.  
  
 커서 라이브러리는 **SQLGetDescRec** 를 실행 하 여 책갈피 열에 대 한 메타 데이터를 반환 합니다. 커서 라이브러리는 **SQLGetDescField** 를 실행 하 여 **SQLGetDescRec**에서 반환 된 것과 동일한 필드를 반환 합니다 .이 필드는 SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_NULLABLE입니다. 일관성을 위해 **SQLGetDescField** 는 SQL_DESC_UNNAMED도 반환 합니다.  
  
 커서 라이브러리는 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_LENGTH 바인딩 책갈피 열에 대해 설정 된 다음 필드의 값을 반환 하기 위해 호출 될 때 **SQLGetDescField** 를 실행 합니다.  
  
 커서 라이브러리는 SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환 하기 위해 호출 될 때 **SQLGetDescField** 를 실행 합니다. 이러한 필드는 책갈피 행 뿐만 아니라 모든 행에 대해 반환 될 수 있습니다.  
  
 응용 프로그램에서 **SQLGetDescField** 를 호출 하 여 앞에서 언급 한 것과 다른 필드의 값을 반환 하는 경우 커서 라이브러리는 해당 호출을 드라이버에 전달 합니다.
