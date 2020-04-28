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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289219"
---
# <a name="table-name-limitations"></a>테이블 이름 제한 사항
테이블 이름에는 모든 유효한 문자 (예: 공백)를 사용할 수 있습니다. 문자, 숫자 및 밑줄을 제외한 모든 문자를 포함 하는 테이블 이름에는 백슬래시 (')로 구분 하 여 구분 해야 합니다.  
  
 Microsoft Excel 드라이버를 사용 하 고 테이블 이름을 데이터베이스 참조로 정규화 되지 않은 경우 기본 데이터베이스가 포함 됩니다. Microsoft Excel에서 이름에 "!" 문자가 포함 된 경우 자동으로 "$" 문자로 변환 됩니다.  
  
 파일 이름>를 참조 \<하는 microsoft excel 테이블 이름은 microsoft excel 3.0 및 4.0 파일에 대해 지원 됩니다. 통합 문서 이름>를 참조 \<하는 microsoft excel 테이블 이름은 microsoft excel 5.0, 7.0 또는 97 파일에 대해 지원 됩니다.  
  
 DBASE 드라이버를 사용 하는 경우 ASCII 값이 127 보다 큰 문자는 밑줄로 변환 됩니다.  
  
 Microsoft Access 드라이버를 사용 하는 경우 테이블 이름은 64 자로 제한 됩니다.  
  
 DBASE, Microsoft Excel 3.0 또는 4.0, Paradox 또는 텍스트 드라이버를 사용 하는 경우 특수 한 MS-DOS 키워드 CON, AUX, LPT1 및 LPT2를 테이블 이름으로 사용 하면 안 됩니다.
