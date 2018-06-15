---
title: INSERT 문의 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f15f7c8a45593b86f50ac4da3dc254dca507aae7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904458"
---
# <a name="insert-statement-limitations"></a>INSERT 문의 제한 사항
삽입된 된 데이터가 너무 길어 열에 맞지 않으면 경고 없이 오른쪽에서 잘립니다.  
  
 가 열의 데이터 형식 범위를 벗어난 값을 삽입 하려고 하면 NULL을 열에 삽입 합니다.  
  
 DBASE, Microsoft Excel, Paradox, 또는 Textdriver를 사용 하면 열에 길이가 0 인 문자열을 삽입 실제로 삽입 NULL 대신 합니다.  
  
 빈 문자열이 null 인 경우 변환 됩니다 Microsoft Excel 드라이버를 사용 하면 빈 문자열은 열에 삽입 하는 경우, 검색 된 SELECT 문의 WHERE 절에는 빈 문자열에서 실행 되는 해당 열에 실패 합니다.  
  
 테이블은 두 가지 조건 Paradox 드라이버에 의해 업데이트할 수 없습니다.  
  
-   경우 고유 인덱스가 테이블에 정의 되지 않았습니다. 고유 인덱스는 테이블에 정의 되어 있지 않더라도 단일 행으로 업데이트할 수 있는 빈 테이블에 대 한 그렇지 않습니다. 단일 행이 고유 인덱스 없는 빈 테이블에 삽입, 응용 프로그램 고유 인덱스를 만들 하거나 단일 행 삽입 한 후 추가 데이터를 삽입할 수 없습니다.  
  
-   Borland 데이터베이스 엔진 구현 되지 않은 경우 읽기 및 추가 문은 Paradox 테이블에서 허용 됩니다.  
  
 텍스트 드라이버를 사용 하면 NULL 값 고정 길이 파일에 빈 값을 채우는 문자열로 표시 되지만 구분 기호로 분리 된 파일에 공백 없음 표시 됩니다. 예를 들어 세 개의 필드가 포함 된 다음 행에서 두 번째 필드는 NULL 값:  
  
```  
"Smith:,, 123  
```  
  
 텍스트 드라이버를 사용 하면 모든 열 값 선행 공백이 채워질 수 있습니다. 모든 행의 길이 보다 작거나 65,543 바이트가 하 여야 합니다.
