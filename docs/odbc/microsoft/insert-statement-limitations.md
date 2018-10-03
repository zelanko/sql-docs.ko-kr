---
title: INSERT 문 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26d4be96ca4dabebd93ee96e2888e18d39257412
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610341"
---
# <a name="insert-statement-limitations"></a>INSERT 문 제한 사항
삽입 된 데이터는 너무 길어 열에 맞지 않을 경우 경고 없이 오른쪽에서 잘립니다.  
  
 열의 데이터 형식 범위를 벗어난 값을 삽입 하려고 하면 열에 삽입할 NULL.  
  
 DBASE, Microsoft Excel, Paradox, 또는 Textdriver를 사용 하면 열에 길이가 0 인 문자열을 삽입 실제로 삽입 NULL 대신 합니다.  
  
 빈 문자열을 NULL 변환할 Microsoft Excel 드라이버를 사용 하면 빈 문자열 열에 삽입 하는 경우, 해당 열에 WHERE 절에 빈 문자열을 사용 하 여 실행 되는 SELECT 문의 검색된에 실패 합니다.  
  
 테이블은 두 가지 조건 Paradox 드라이버에 의해 업데이트할 수 없습니다.  
  
-   경우 고유 인덱스를 테이블에 정의 되지 않았습니다. 이 고유 인덱스를 테이블에 정의 되어 있지 않더라도 단일 행을 사용 하 여 업데이트할 수 있는 빈 테이블에 대 한 그렇지 않습니다. 단일 행을 고유 인덱스가 없는 빈 테이블에 삽입 하는 경우 응용 프로그램 고유 인덱스를 만들 수 없습니다. 또는 단일 행을 삽입 한 후에 추가 데이터를 삽입 합니다.  
  
-   Borland 데이터베이스 엔진 구현 되지 않은 경우 읽기 및 추가 Paradox 테이블에서 문을 사용할 수 있습니다.  
  
 텍스트 드라이버를 사용 하면 NULL 값 고정 길이 파일에 빈 값으로 채워집니다 문자열로 표현 됩니다 있지만 구분 기호로 분리 된 파일에 공백이 표시 됩니다. 예를 들어 세 개의 필드가 포함 된 다음 행에서 두 번째 필드는 NULL 값:  
  
```  
"Smith:,, 123  
```  
  
 텍스트 드라이버를 사용 하면 모든 열 값 선행 공백을 사용 하 여 채워질 수 있습니다. 모든 행의 길이 보다 작거나 65,543 바이트가 하 여야 합니다.
