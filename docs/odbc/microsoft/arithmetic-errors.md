---
title: 산술 오류 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab1b472540d1978a6e7a06d94da7542cc641e999
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299903"
---
# <a name="arithmetic-errors"></a>산술 오류
ODBC 드라이버는 SELECT 문의 WHERE 절을 각 행을 가져올 때 평가합니다. 행에 0분할 또는 숫자 오버플로와 같은 산술 오류를 일으키는 값이 포함된 경우 드라이버는 모든 행을 반환하지만 산술 오류가 있는 열에 대한 오류를 반환합니다. 그러나 삽입 하거나 업데이트 할 때 ODBC 드라이버는 첫 번째 산술 오류가 발생 하면 데이터 삽입 또는 업데이트를 중지 합니다.
