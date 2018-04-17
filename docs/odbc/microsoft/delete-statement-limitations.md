---
title: DELETE 문의 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 45386d8278e968b55fba5881dfe9b914bc23f454
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="delete-statement-limitations"></a>DELETE 문의 제한 사항
Microsoft Excel 또는 텍스트 드라이버에 대 한 DELETE 문은 지원 되지 않습니다. 참고는 INSERT 문이 텍스트 드라이버에 대 한 지원 됩니다.  
  
 DBASE 드라이버 "deleted" 값을 제거 하려면 테이블을 압축 하는 것을 지원 하지 않습니다.  
  
 테이블에서 행을 삭제 하려면 Paradox 드라이버에 대 한 테이블에 고유 인덱스 (기본 키 Paradox) 있어야 합니다.
