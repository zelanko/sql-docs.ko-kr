---
title: 다국어 기능 지원 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 151d3989737d221e46f6771055d0775c69f7e576
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>다국어 기능 지원 (Visual FoxPro ODBC 드라이버)
Microsoft Visual FoxPro ODBC 드라이버를 지원합니다.  
  
-   더블 바이트 문자 집합 (DBCS)  
  
-   여러 데이터 정렬 시퀀스  
  
 데이터 정렬 순서를 정의 고 *정렬 순서* Visual FoxPro 테이블 또는 데이터베이스에 저장 된 데이터에 대 한 합니다. 기본적으로 드라이버가 운영 체제의 언어 버전을 지 원하는 데이터 정렬 순서를 사용 하도록 구성 됩니다.  
  
 목록이 지원 되는 데이터 정렬 시퀀스에 대 한 참조 [COLLATE 설정](../../odbc/microsoft/set-collate-command.md)합니다.  
  
## <a name="locale"></a>로캘(locale)  
 지정 된 언어 및 국가/지역에 해당 하는 정보의 집합입니다. 로캘의 소수 구분 기호, 날짜 및 시간 형식 및 문자 정렬 순서 등의 특정 설정을 나타냅니다.  
  
## <a name="sort-order"></a>정렬 순서(sort order)  
 다른 정렬 규칙을 통합 하는 정렬 순서 *로캘*s, 해당 언어의 데이터를 올바르게 정렬할 수 있습니다. Visual FoxPro 현재 정렬 순서는 결과 문자 식 비교와 레코드에 표시 된 인덱스 또는 테이블을 정렬 순서를 결정 합니다.
