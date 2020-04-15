---
title: 데이터 유형 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280673"
---
# <a name="data-type-limitations"></a>데이터 형식 제한 사항
Microsoft ODBC 데스크톱 데이터베이스 드라이버는 데이터 형식에 다음과 같은 제한 사항이 적용됩니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|모든 데이터 형식|형식 변환 실패로 인해 영향을 받는 열이 NULL로 설정될 수 있습니다.|  
|BINARY|0 길이 의 BINARY 열을 만들면 실제로 255바이트 BINARY 열을 반환합니다.|  
|DATE|DATE 데이터 형식은 CONVERT 함수에 의해 다른 데이터 형식(또는 자체)으로 변환할 수 없습니다.|  
|소수점(정확한 숫자)|지원되지 않습니다.|  
|부동 지점 데이터 유형|부동 소수점 번호의 소수 자릿수는 Windows 제어판의 국제 섹션에 설정된 숫자 형식에 따라 제한될 수 있습니다.|  
|NUMERIC|최대 정밀도와 28의 배율을 지원합니다.|  
|timestamp|CONVERT 함수에서 TIMESTAMP 데이터 형식을 자체적으로 변환할 수 없습니다.|  
|TINYINT|TINYINT 값은 항상 서명되지 않습니다.|  
|길이가 0인 문자열|dBASE, Microsoft Excel, 역설 또는 Textdriver를 사용하면 0 길이 문자열을 열에 삽입하면 실제로 NULL이 삽입됩니다.|
