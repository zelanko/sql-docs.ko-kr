---
title: 테이블 이름 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289219"
---
# <a name="table-name-limitations"></a>테이블 이름 제한 사항
테이블 이름에는 유효한 문자(예: 공백)가 포함될 수 있습니다. 테이블 이름에 문자, 숫자 및 밑줄을 제외한 문자가 포함된 경우 이름을 다시 따옴표(')로 둘러싸서 이름을 구분해야 합니다.  
  
 Microsoft Excel 드라이버를 사용하고 테이블 이름이 데이터베이스 참조로 정규화되지 않은 경우 기본 데이터베이스가 암시됩니다. Microsoft Excel의 이름에 "!" 문자가 포함되어 있으면 자동으로 "$" 문자로 변환됩니다.  
  
 파일 이름> 참조하는 \<Microsoft Excel 테이블 이름은 Microsoft Excel 3.0 및 4.0 파일에 대해 지원됩니다. 통합 문서 이름> \<참조하는 Microsoft Excel 테이블 이름은 Microsoft Excel 5.0, 7.0 또는 97 파일에 대해 지원됩니다.  
  
 dBASE 드라이버를 사용하면 ASCII 값이 127보다 큰 문자가 밑줄로 변환됩니다.  
  
 Microsoft Access 드라이버를 사용하면 테이블 이름이 64자로 제한됩니다.  
  
 dBASE, Microsoft Excel 3.0 또는 4.0, 역설 또는 텍스트 드라이버를 사용하는 경우 특수 MS-DOS 키워드 CON, AUX, LPT1 및 LPT2를 테이블 이름으로 사용해서는 안 됩니다.
