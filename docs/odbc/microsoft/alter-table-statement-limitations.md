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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19afa8b07b0051de9ce45ec652ea337c0f689f52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304702"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE 문 제한 사항
DBASE 또는 Paradox 드라이버를 사용 하는 경우 인덱스를 만들고 새 레코드를 추가한 후에는 인덱스를 삭제 하 고 테이블의 내용을 삭제 하지 않는 한 ALTER TABLE 문을 사용 하 여 테이블 구조를 변경할 수 없습니다.  
  
 Microsoft Excel 또는 텍스트 드라이버에는 ALTER TABLE 문이 지원 되지 않습니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진를 구현 하지 않고 Paradox 드라이버를 사용 하는 경우 ALTER TABLE 문은 지원 되지 않습니다. 읽기 및 추가 문만 사용할 수 있습니다.
