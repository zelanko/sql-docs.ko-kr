---
title: ALTER TABLE 문 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02ce530385cdc911250a81d831dd2fdb81873f76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301981"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 문 제한 사항
DBASE 또는 Paradox 드라이버는 사용 경우 인덱스를 만든 후 새 레코드를 추가, 인덱스가 삭제 됩니다 하 고 테이블의 내용을 삭제 하지 않으면 ALTER TABLE 문에서 테이블의 구조를 변경할 수 없습니다.  
  
 Microsoft Excel 또는 텍스트 드라이버에 대 한 ALTER TABLE 문은 지원 되지 않습니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진을 구현 하지 않고도 Paradox 드라이버를 사용 하는 경우 ALTER TABLE 문은 지원 되지 않습니다. 읽기 및 추가 문이 허용 됩니다.
