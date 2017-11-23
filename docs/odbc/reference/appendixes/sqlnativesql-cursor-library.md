---
title: "SQLNativeSql (커서 라이브러리) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1541b22f68dabdc5f5425346fe83da7adf2ee83
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLNativeSql** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLNativeSql**, 참조 [SQLNativeSql 함수](../../../odbc/reference/syntax/sqlnativesql-function.md)합니다.  
  
 커서 라이브러리를 호출 하는 드라이버에서이 기능을 지 원하는 경우 **SQLNativeSql** 드라이버에서 SQL 문에 전달 합니다. 위치 지정된 업데이트에 대 한 delete, 배치 및 **업데이트에 대 한 선택** 문을 커서 라이브러리 문을 수정 하 여 드라이버에 전달 하기 전에.  
  
> [!NOTE]  
>  커서 라이브러리 잘못 반환한 SQLSTATE 34000 (잘못 된 커서 이름) 위치 지정된 업데이트 또는 delete 문에 전달 되는 커서 이름이 유효 하지 않은 *InStatementText* 의 인수 **SQLNativeSql** . **SQLNativeSql** 문 준비 또는 실행 될 경우에 반환 되는 구문 오류를 반환 하기 위한 용도가 아닙니다.
