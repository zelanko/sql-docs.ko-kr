---
title: UPDATE 문 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cc8cf58d4e4d826dc4b152e395dedbea395a095
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088199"
---
# <a name="update-statement-limitations"></a>UPDATE 문 제한 사항
테이블을 업데이트할 Paradox 드라이버에 대 한 고유 인덱스 (Paradox 기본 키) 테이블에 있어야 합니다. Borland 데이터베이스 엔진을 구현 하지 않고도 Paradox 드라이버를 사용 하는 경우 Paradox 테이블을 업데이트 하는 것이 불가능 합니다.  
  
 텍스트 드라이버에서 지원 되지 않습니다.  
  
 Microsoft Excel 드라이버를 사용 하면 값을 업데이트할 수 있지만 Microsoft Excel 스프레드시트에 따라 테이블에서 행을 삭제할 수 없습니다. 따라서 UPDATE 문은 Microsoft Excel 드라이버에서 공식적으로 지원을 고려 하지 않습니다. INSERT 문만 지원 되는 것으로 간주 됩니다.
