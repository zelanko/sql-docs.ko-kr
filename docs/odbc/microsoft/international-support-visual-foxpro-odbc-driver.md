---
title: 국제 지원 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e987c224f2d716fcab3bf898b1cb276e922e48ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085499"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>다국어 기능 지원(Visual FoxPro ODBC 드라이버)
Microsoft Visual FoxPro ODBC 드라이버는 다음을 지원 합니다.  
  
-   DBCS (더블 바이트 문자 집합)  
  
-   여러 정렬 시퀀스  
  
 데이터 정렬 순서는 Visual FoxPro 테이블 또는 데이터베이스에 저장 된 데이터에 대 한 *정렬 순서* 를 정의 합니다. 기본적으로 드라이버는 운영 체제의 언어 버전을 지 원하는 데이터 정렬 순서를 사용 하도록 구성 됩니다.  
  
 지원 되는 데이터 정렬 순서 목록은 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)을 참조 하세요.  
  
## <a name="locale"></a>locale  
 지정 된 언어 및 국가/지역에 해당 하는 정보 집합입니다. 로캘은 소수 구분 기호, 날짜 및 시간 형식, 문자 정렬 순서 등의 특정 설정을 나타냅니다.  
  
## <a name="sort-order"></a>정렬 순서(sort order)  
 정렬 순서는 다른 *로캘의*정렬 규칙을 통합 하 여 해당 언어의 데이터를 올바르게 정렬할 수 있도록 합니다. Visual FoxPro에서 현재 정렬 순서는 문자 식 비교 결과와 레코드가 인덱싱된 테이블 또는 정렬 된 테이블에 표시 되는 순서를 결정 합니다.
