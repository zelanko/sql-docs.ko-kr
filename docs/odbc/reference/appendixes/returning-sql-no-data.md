---
title: SQL_NO_DATA를 반환 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2f731589dcbc10d24ff42d895db60f9f8c054de
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794179"
---
# <a name="returning-sqlnodata"></a>SQL_NO_DATA 반환
때 ODBC *2.x* ODBC 응용 프로그램 사용 *3.x* 드라이버 호출 **SQLExecDirect**하십시오 **SQLExecute**, 또는  **SQLParamData**, 및 검색된 update 또는 delete 문이 실행 된 ODBC 데이터 소스의 모든 행에는 영향을 주지 않았습니다 *3.x* 드라이버와 관계 없이 SQL_SUCCESS를 반환 해야 합니다. 때 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *3.x* 드라이버 호출 **SQLExecDirect**하십시오 **SQLExecute**, 또는  **SQLParamData** 와 동일한 결과 ODBC *3.x* 드라이버에서 SQL_NO_DATA를 반환 해야 합니다.  
  
 검색 한 update 또는 delete에 문 일괄 처리 문의 영향을 받지 않습니다 데이터 소스의 모든 행 **SQLMoreResults** 관계 없이 SQL_SUCCESS를 반환 합니다. 더 이상 결과가 없습니다 있는지 검색된 업데이트/삭제 행이 없는 받는에서 결과 의미 때문에 SQL_NO_DATA를 반환할 수 없습니다.
