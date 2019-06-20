---
title: 테이블 이름 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31c1703bc03a2881e7b9b96989b8949cc81aba7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63226341"
---
# <a name="table-name-limitations"></a>테이블 이름 제한 사항
테이블 이름 (예를 들어, 공백) 유효한 문자를 포함할 수 있습니다. 테이블 이름은 문자, 숫자 및 밑줄을 제외한 모든 문자가 들어 있는 경우 백 따옴표 (')에 포함 하 여 이름을 구분 해야 합니다.  
  
 Microsoft Excel 드라이버를 사용 하는 테이블 이름을 데이터베이스 참조로 정규화 되지 않은 경우 기본 데이터베이스는 포함 됩니다. Microsoft Excel에서 이름을 포함 하는 경우는 "!" 문자를 "$" 문자 대신 변환 자동으로 됩니다.  
  
 참조 하는 Microsoft Excel 테이블 이름 \<파일 이름 > Microsoft Excel 3.0 및 4.0 파일 지원 됩니다. 참조 하는 Microsoft Excel 테이블 이름 \<통합 문서 이름 > 5.0, 7.0, 또는 97 Microsoft Excel 파일에 대 한 지원 됩니다.  
  
 DBASE 드라이버를 사용 하면 ASCII 값이 127 보다 큰 문자는 밑줄으로 변환 됩니다.  
  
 Microsoft Access 드라이버를 사용 하는 경우 테이블 이름은 64 자로 제한 됩니다.  
  
 DBASE, 3.0 또는 4.0, Paradox, 또는 텍스트 Microsoft Excel 드라이버를 사용 하면 CON, AUX, LPT1, LPT2 특수 MS-DOS 키워드는 테이블 이름으로 사용할 수 없습니다.
