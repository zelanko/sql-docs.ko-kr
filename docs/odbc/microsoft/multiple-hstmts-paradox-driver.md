---
title: 여러 hstmts (역설 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac381024a6b4b67719cb7c098367f63a6176bad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298193"
---
# <a name="multiple-hstmts-paradox-driver"></a>다중 hstmts(Paradox 드라이버)
ODBC 역설 드라이버를 사용하는 경우 테이블에서 쿼리를 실행하기 위해 두 개 이상의 *hstmt를* 사용하려면 테이블에 고유한 인덱스(Paradox 기본 키)가 있어야 합니다.
