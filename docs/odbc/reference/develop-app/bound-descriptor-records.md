---
title: 바운드 된 설명자 레코드 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 155ef4951abddc7a73d9d4abfbc45248f33d653c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306310"
---
# <a name="bound-descriptor-records"></a>바인딩된 설명자 레코드
응용 프로그램이 더 이상 null 값을 포함하지 않도록 설명자 레코드의 SQL_DESC_DATA_PTR 필드를 설정하면 레코드가 *바인딩된*것으로 합니다.  
  
 설명자가 APD인 경우 각 바인딩된 레코드는 바인딩된 매개 변수를 구성합니다. 입력 매개 변수의 경우 응용 프로그램은 문을 실행하기 전에 SQL 문의 각 동적 매개 변수 마커에 대한 매개 변수를 바인딩해야 합니다. 출력 매개 변수의 경우 응용 프로그램이 매개 변수를 바인딩할 필요가 없습니다.  
  
 설명자가 데이터베이스 데이터 행을 설명하는 ARD인 경우 각 바인딩된 레코드는 바인딩된 열을 구성합니다.
