---
title: SQLNativeSql (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c42efbd87296cf7157d75d1848e4655247818
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125705"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLNativeSql** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLNativeSql**를 참조 하십시오 [SQLNativeSql 함수](../../../odbc/reference/syntax/sqlnativesql-function.md)합니다.  
  
 커서 라이브러리를 호출 하는 드라이버에서이 함수를 지 원하는 경우 **SQLNativeSql** 드라이버에서 SQL 문에 전달 합니다. 위치 지정된 업데이트에 대 한 삭제를 배치 하 고 **업데이트에 대 한 선택** 문을 커서 라이브러리 문을 수정 하 여 드라이버에 전달 하기 전에 합니다.  
  
> [!NOTE]  
>  커서 라이브러리를 잘못 반환한 SQLSTATE 34000 (잘못 된 커서 이름)의 위치 지정된 update 또는 delete 문에 전달 되는 커서 이름이 올바르지 않으면 합니다 *InStatementText* 인수의 **SQLNativeSql** . **SQLNativeSql** 문 준비 또는 실행 될 경우에 반환 되는 구문 오류를 반환할 수 없습니다.
