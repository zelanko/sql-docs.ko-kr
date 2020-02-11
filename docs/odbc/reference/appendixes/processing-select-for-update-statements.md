---
title: SELECT FOR UPDATE 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ad9a20ab8abd40123ec4e4d7369373e68699205
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028370"
---
# <a name="processing-select-for-update-statements"></a>SELECT FOR UPDATE 문 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 상호 운용성을 최대화 하기 위해 응용 프로그램은 **SELECT FOR update** 문을 실행 하 여 위치 지정 update 문으로 업데이트 되는 결과 집합을 생성 해야 합니다. 커서 라이브러리에는이 작업이 필요 하지 않지만 위치 지정 update 문을 지 원하는 대부분의 데이터 원본에 필요 합니다.  
  
 커서 라이브러리는 **SELECT for** Update 문의 **for update** 절에 있는 열을 무시 합니다. 문을 드라이버에 전달 하기 전에이 절을 제거 합니다. 커서 라이브러리에서, 이전 섹션에서 언급 한 제한과 함께 SQL_ATTR_CONCURRENCY statement 특성은 결과 집합의 열을 업데이트할 수 있는지 여부를 제어 합니다.
