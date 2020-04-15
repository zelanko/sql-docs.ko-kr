---
title: 업데이트 설명서에 대한 선택 처리 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 904028cd7b3798fcac8f9e5afa6186fae3e9fa29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308014"
---
# <a name="processing-select-for-update-statements"></a>SELECT FOR UPDATE 문 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 최대 상호 운용성을 위해 응용 프로그램은 SELECT FOR UPDATE 문을 실행하여 위치 가 있는 업데이트 문으로 업데이트되는 결과 **집합을** 생성해야 합니다. 커서 라이브러리에는 이 작업이 필요하지 않지만 위치가 있는 업데이트 문을 지원하는 대부분의 데이터 원본이 필요합니다.  
  
 커서 라이브러리는 UPDATE 용 **SELECT** 문의 **FOR UPDATE** 절의 열을 무시합니다. 드라이버에 문을 전달하기 전에 이 절을 제거합니다. 커서 라이브러리에서 SQL_ATTR_CONCURRENCY 문 특성은 이전 섹션에서 언급한 제한 사항과 함께 결과 집합의 열을 업데이트할 수 있는지 여부를 제어합니다.
