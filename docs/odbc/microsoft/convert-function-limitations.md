---
title: 변환 기능 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, CONVERT function limitations
- Convert function limitations [ODBC]
ms.assetid: 3c81fc58-57f0-4dd7-be16-2b146eb15cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f4258e737327ae11f03a96cfef3cdecf133e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281033"
---
# <a name="convert-function-limitations"></a>CONVERT 함수 제한 사항
형식 변환 실패로 인해 영향을 받는 열이 NULL로 설정됩니다.  
  
 날짜 또는 TIMESTAMP 데이터 형식은 CONVERT 함수에 의해 다른 데이터 형식(또는 자체)으로 변환할 수 없습니다.
