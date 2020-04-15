---
title: 업데이트 성명서 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307624"
---
# <a name="update-statement-limitations"></a>UPDATE 문 제한 사항
패러독스 드라이버가 테이블을 업데이트하려면 테이블에 고유한 인덱스(역설 기본 키)가 있어야 합니다. Borland 데이터베이스 엔진을 구현하지 않고 역설 드라이버를 사용하는 경우 역설 테이블을 업데이트할 수 없습니다.  
  
 텍스트 드라이버에서 지원되지 않습니다.  
  
 Microsoft Excel 드라이버를 사용하면 값을 업데이트할 수 있지만 Microsoft Excel 스프레드시트를 기반으로 하는 테이블에서 행을 삭제할 수 없습니다. 따라서 UPDATE 문은 Microsoft Excel 드라이버에서 공식적으로 지원하는 것으로 간주되지 않습니다. INSERT 문만 지원되는 것으로 간주됩니다.
