---
title: ALTER 테이블 문 제한 사항 | Microsoft Docs
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
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06af545611da90d51ad0fc82136a4cb1ecc3984c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table-statement-limitations"></a>ALTER 테이블 문 제한 사항
DBASE 또는 Paradox 드라이버는 사용 경우 만든 후에 인덱스에 새 레코드가 추가 인덱스를 삭제 하 고 테이블의 내용이 삭제 하지 않으면 ALTER TABLE 문에서 테이블의 구조를 변경할 수 없습니다.  
  
 Microsoft Excel 또는 텍스트 드라이버에 대 한 ALTER TABLE 문은 지원 되지 않습니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진을 구현 하지 않고 Paradox 드라이버를 사용 하는 경우 ALTER TABLE 문은 지원 되지 않습니다. 읽기 및 추가 하는 문을 사용할 수 있습니다.
