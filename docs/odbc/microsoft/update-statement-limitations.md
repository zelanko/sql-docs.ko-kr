---
title: UPDATE 문의 제한 사항 | Microsoft Docs
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
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca36c4ae277aa36e9cbf2e4787b6131ce099ce17
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="update-statement-limitations"></a>UPDATE 문의 제한 사항
테이블을 업데이트할 Paradox 드라이버에 대 한 테이블에 고유 인덱스 (기본 키 Paradox) 있어야 합니다. Borland 데이터베이스 엔진을 구현 하지 않고 Paradox 드라이버를 사용 하는 경우 Paradox 테이블을 업데이트 하는 것이 불가능 합니다.  
  
 텍스트 드라이버에서 지원 되지 않습니다.  
  
 Microsoft Excel 드라이버 사용 되는 값을 업데이트할 수는 있지만 Microsoft Excel 스프레드시트를 기준으로 테이블에서 행을 삭제할 수 없습니다. 결과적으로, UPDATE 문이 Microsoft Excel 드라이버에서 공식적으로 지원을 간주 되지 않습니다. INSERT 문의 지 원하는 것으로 간주 됩니다.
