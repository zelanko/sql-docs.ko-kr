---
title: "읽기 전용 상태 (Excel 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2778444177477548a28b4139b6ba4bdb3bdea6fa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="read-only-status-excel-driver"></a>읽기 전용 상태 (Excel 드라이버)
Microsoft Excel 드라이버를 사용 하면 데이터 원본 테이블 읽기 전용으로 기본적으로 열리고 한 번에 한 명의 사용자만 열 수 있습니다. 그러나 테이블을 확보 하더라도 읽기 전용 상태 응용 프로그램을 수행할 수는 삽입 및 업데이트 Microsoft Excel 테이블에 대 한 합니다.  
  
 Microsoft Excel 드라이버를 통해 Microsoft Excel 데이터에 대해 다른 이름으로 저장 명령을 수행 하는 응용 프로그램, 응용 프로그램이 새 테이블 만들고 새 테이블에 저장 되도록 데이터를 삽입 해야 합니다. 삽입 될 테이블에 추가 합니다. 닫고 다시 될 때까지 테이블에 없는 다른 작업을 수행할 수 있습니다. 테이블을 닫은 후 읽기 전용 테이블은 다음 이므로 없습니다 후속 insert는 수행할 수 있습니다.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 값을 업데이트할 수 있지만 Microsoft Excel 스프레드시트를 공식적으로 Microsoft Excel 드라이버에서 지 원하는 업데이트 된 것으로 간주 되지 기준으로 테이블에서 행을 삭제할 수 없습니다.
