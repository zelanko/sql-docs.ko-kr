---
title: 국제 지원 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4b0c758bb478ea6a468e6756c3d6f0f52c766f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299973"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>다국어 기능 지원(Visual FoxPro ODBC 드라이버)
마이크로소프트 비주얼 폭스프로 ODBC 드라이버 지원:  
  
-   이중 바이트 문자 세트(DBCS)  
  
-   여러 개의 정렬 시퀀스  
  
 데이터 정렬 시퀀스는 Visual FoxPro 테이블 또는 데이터베이스에 저장된 데이터의 *정렬 순서를* 정의합니다. 기본적으로 드라이버는 운영 체제의 언어 버전을 지원하는 정렬 시퀀스를 사용하도록 구성됩니다.  
  
 지원되는 정렬 시퀀스 목록은 [COLLATE SET을](../../odbc/microsoft/set-collate-command.md)참조하십시오.  
  
## <a name="locale"></a>locale  
 지정된 언어 및 국가/지역에 해당하는 정보 집합입니다. 로캘은 소수점 구분 기호, 날짜 및 시간 형식 및 문자 정렬 순서와 같은 특정 설정을 나타냅니다.  
  
## <a name="sort-order"></a>정렬 순서(sort order)  
 정렬 순서는 서로 다른 *로캘*s의 정렬 규칙을 통합하여 해당 언어로 데이터를 올바르게 정렬할 수 있도록 합니다. Visual FoxPro에서 현재 정렬 순서는 문자 식 비교 결과와 레코드가 인덱싱되거나 정렬된 테이블에 표시되는 순서를 결정합니다.
