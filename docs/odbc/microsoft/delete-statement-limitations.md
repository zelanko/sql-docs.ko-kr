---
title: DELETE 문 제한 사항 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303534"
---
# <a name="delete-statement-limitations"></a>DELETE 문 제한 사항
Microsoft Excel 또는 텍스트 드라이버에는 DELETE 문을 사용할 수 없습니다. 텍스트 드라이버에는 INSERT 문이 지원 됩니다.  
  
 DBASE 드라이버는 "삭제 된" 값을 제거 하는 테이블 압축을 지원 하지 않습니다.  
  
 Paradox 드라이버가 테이블에서 행을 삭제 하려면 테이블에 고유 인덱스 (Paradox 기본 키)가 있어야 합니다.
