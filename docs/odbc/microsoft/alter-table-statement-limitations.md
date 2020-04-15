---
title: 테이블 설명 제한 변경 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304702"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 문 제한 사항
dBASE 또는 Paradox 드라이버를 사용하면 인덱스가 만들어지고 새 레코드가 추가되면 인덱스가 삭제되고 테이블의 내용이 삭제되지 않는 한 ALTER TABLE 문으로 테이블 구조를 변경할 수 없습니다.  
  
 ALTER TABLE 문은 Microsoft Excel 또는 텍스트 드라이버에 대해 지원되지 않습니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진을 구현하지 않고 역설 드라이버를 사용하는 경우 ALTER TABLE 문은 지원되지 않습니다. 읽기 및 부가 문만 허용됩니다.
