---
title: INSERT 문 제한 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f903f15ec13baa28a789891c1527dc742daa68ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300010"
---
# <a name="insert-statement-limitations"></a>INSERT 문 제한 사항
삽입된 데이터는 열에 맞지 않는 시간이 너무 길면 경고 없이 오른쪽에 잘립니다.  
  
 열의 데이터 형식 범위를 벗어난 값을 삽입하려고 하면 NULL이 열에 삽입됩니다.  
  
 dBASE, Microsoft Excel, 역설 또는 Textdriver를 사용하면 0 길이 문자열을 열에 삽입하면 실제로 NULL이 삽입됩니다.  
  
 Microsoft Excel 드라이버를 사용하면 빈 문자열이 열에 삽입되면 빈 문자열이 NULL로 변환됩니다. WHERE 절의 빈 문자열로 실행되는 검색된 SELECT 문은 해당 열에서 성공하지 못합니다.  
  
 다음 두 조건에서 역설 드라이버에 의해 테이블이 업데이터화되지 않습니다.  
  
-   테이블에 고유 인덱스가 정의되지 않은 경우 테이블에 고유한 인덱스가 정의되어 있지 않더라도 단일 행으로 업데이트할 수 있는 빈 테이블에는 해당되지 않습니다. 고유한 인덱스가 없는 빈 테이블에 단일 행이 삽입된 경우 응용 프로그램은 고유한 인덱스를 만들거나 단일 행을 삽입한 후 추가 데이터를 삽입할 수 없습니다.  
  
-   Borland 데이터베이스 엔진이 구현되지 않은 경우 Paradox 테이블에서 읽기 및 부속 문만 허용됩니다.  
  
 Text 드라이버를 사용하면 NULL 값은 고정 길이 파일의 빈 패딩 문자열로 표시되지만 제한된 파일에공백이 표시되지 않습니다. 예를 들어 세 개의 필드가 포함된 다음 행에서 두 번째 필드는 NULL 값입니다.  
  
```  
"Smith:,, 123  
```  
  
 Text 드라이버를 사용하면 모든 열 값을 선행 공백으로 패딩할 수 있습니다. 행의 길이는 65,543바이트 보다 적거나 같아야 합니다.
