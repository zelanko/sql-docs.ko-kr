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
ms.openlocfilehash: 1676af6216ac703e9a8976951ec2888b9e940b67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085519"
---
# <a name="insert-statement-limitations"></a>INSERT 문 제한 사항
삽입 된 데이터는 너무 길어서 열에 맞지 않는 경우 경고 없이 오른쪽에서 잘립니다.  
  
 열 데이터 형식의 범위를 벗어난 값을 삽입 하려고 하면 NULL이 열에 삽입 됩니다.  
  
 DBASE, Microsoft Excel, Paradox 또는 Textdriver를 사용 하는 경우 열에 길이가 0 인 문자열을 삽입 하면 실제로 NULL이 삽입 됩니다.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 빈 문자열을 열에 삽입 하면 빈 문자열이 NULL로 변환 됩니다. WHERE 절에서 빈 문자열을 사용 하 여 실행 되는 검색 된 SELECT 문은 해당 열에서 실패 합니다.  
  
 다음 두 가지 조건에서 Paradox 드라이버가 테이블을 업데이트할 수 없습니다.  
  
-   테이블에 고유 인덱스가 정의 되어 있지 않은 경우 이는 테이블에 고유 인덱스가 정의 되어 있지 않은 경우에도 단일 행으로 업데이트할 수 있는 빈 테이블에는 적용 되지 않습니다. 고유 인덱스가 없는 빈 테이블에 단일 행을 삽입 하는 경우 응용 프로그램은 단일 행이 삽입 된 후에 고유한 인덱스를 만들거나 추가 데이터를 삽입할 수 없습니다.  
  
-   Borland 데이터베이스 엔진 구현 되지 않은 경우에는 Paradox 테이블에 읽기 및 추가 문만 사용할 수 있습니다.  
  
 텍스트 드라이버를 사용 하는 경우 NULL 값은 고정 길이 파일에서 빈 패딩 문자열로 표시 되지만 구분 기호로 분리 된 파일에는 공백으로 표시 됩니다. 예를 들어 세 개의 필드가 포함 된 다음 행에서 두 번째 필드는 NULL 값입니다.  
  
```  
"Smith:,, 123  
```  
  
 텍스트 드라이버를 사용 하는 경우 모든 열 값은 선행 공백으로 채워질 수 있습니다. 행의 길이는 65543 바이트 보다 작거나 같아야 합니다.
