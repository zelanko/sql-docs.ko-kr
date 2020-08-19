---
description: SQL_NO_DATA 반환
title: SQL_NO_DATA 반환 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24efdd88d16ba31a2b70dfb75ad21adee08c6f1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424975"
---
# <a name="returning-sql_no_data"></a>SQL_NO_DATA 반환
*Odbc 2.x 응용 프로그램* 에서 odbc 셸을 사용 때는 드라이버가 **sqlexecdirect**, **Sqlexecute**또는 **sqlexecdirect**를 호출 하 고 검색 된 update 또는 delete 문이 실행 되었지만 데이터 원본의 어떤 행에도 영향을 주지 않은 경우 odbc *3.x 드라이버는* SQL_SUCCESS을 반환 해야 *합니다.* *Odbc 3.x 드라이버를* 사용 하 여 작업 하는 odbc *3(sp3)* 응용 프로그램에서 동일한 결과를 사용 하 여 **sqlexecdirect**, **sqlexecute**또는 **sqlexecdirect** 를 호출 하는 *경우 odbc 3.x* 드라이버는 SQL_NO_DATA을 반환 해야 합니다.  
  
 문 일괄 처리에서 검색 된 update 또는 delete 문이 데이터 원본의 어떤 행에도 영향을 주지 않으면 **SQLMoreResults** 는 SQL_SUCCESS을 반환 합니다. 결과를 SQL_NO_DATA 반환할 수 없습니다 .이는 더 이상 결과가 없다는 것을 의미 하기 때문입니다. 행에 영향을 미치지 않는 검색 된 업데이트/삭제의 결과가 없다는 것은 아닙니다.
