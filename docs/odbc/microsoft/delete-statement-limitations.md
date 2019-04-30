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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98bd56051c724186d7308eff669263d29b82ecd5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198173"
---
# <a name="delete-statement-limitations"></a>DELETE 문 제한 사항
Microsoft Excel 또는 텍스트 드라이버에 대 한 DELETE 문은 지원 되지 않습니다. INSERT 문의 텍스트 드라이버에 대 한 지원 되는 참고 합니다.  
  
 DBASE 드라이버 "deleted" 값을 제거 하려면 테이블을 압축 하는 것을 지원 하지 않습니다.  
  
 테이블에서 행을 삭제 하려면 Paradox 드라이버에 대 한 고유 인덱스 (Paradox 기본 키) 테이블에 있어야 합니다.
