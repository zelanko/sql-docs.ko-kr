---
title: 삭제 명령문 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365b54ab8c0678253e184b397f1f71e39aed3b9b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303534"
---
# <a name="delete-statement-limitations"></a>DELETE 문 제한 사항
DELETE 문은 Microsoft Excel 또는 텍스트 드라이버에 대해 지원되지 않습니다. INSERT 문은 텍스트 드라이버에 대해 지원됩니다.  
  
 dBASE 드라이버는 "삭제된" 값을 제거하기 위해 테이블 패킹을 지원하지 않습니다.  
  
 패러독스 드라이버가 테이블에서 행을 삭제하려면 테이블에 고유한 인덱스(Paradox 기본 키)가 있어야 합니다.
