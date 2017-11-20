---
title: "데이터 형식 제한 사항 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 558789a4f435e9fc54176b1423d71369f6b4cc22
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-limitations"></a>데이터 형식 제한 사항
Microsoft ODBC 데스크톱 데이터베이스 드라이버 데이터 형식에 대해 다음과 같은 제한 사항이 적용:  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|모든 데이터 형식|형식 변환 실패 영향을 받는 열이 NULL로 설정 되 고 발생할 수 있습니다.|  
|BINARY|길이가 0 인 이진 열을 만들어 실제로 255 바이트 이진 열을 반환 합니다.|  
|DATE|DATE 데이터 형식 변환 함수에 의해 다른 데이터 형식 (또는 자체)로 변환할 수 없습니다.|  
|10 진수 (정확한 수치)|지원되지 않습니다.|  
|부동 소수점 데이터 형식|부동 소수점 숫자에서 소수 자릿수 Windows 제어판의 국가별 섹션에서 설정 하는 숫자 형식에 따라 제한 될 수 있습니다.|  
|NUMERIC|최대 전체 자릿수 및 소수 자릿수는 28 지원합니다.|  
|timestamp|TIMESTAMP 데이터 형식은 CONVERT 함수에서 자기 자신으로 변환할 수 없습니다.|  
|TINYINT|TINYINT 값은 항상 서명 합니다.|  
|길이가 0 인 문자열|DBASE, Microsoft Excel, Paradox, 또는 Textdriver를 사용 하면 열에 길이가 0 인 문자열을 삽입 실제로 삽입 NULL 대신 합니다.|

