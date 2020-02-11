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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125705"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLNativeSql** 함수를 사용 하는 방법을 설명 합니다. **SQLNativeSql**에 대 한 일반 정보는 [SQLNativeSql 함수](../../../odbc/reference/syntax/sqlnativesql-function.md)를 참조 하세요.  
  
 드라이버가이 함수를 지 원하는 경우 커서 라이브러리는 드라이버에서 **SQLNativeSql** 를 호출 하 고이를 SQL 문으로 전달 합니다. 위치 지정 업데이트, 위치 지정 삭제 및 **SELECT FOR update** 문에 대해 커서 라이브러리는 문을 드라이버에 전달 하기 전에 수정 합니다.  
  
> [!NOTE]  
>  **SQLNativeSql**의 현재 위치에 *전달 된 update* 또는 delete 문에서 커서 이름이 잘못 된 경우 커서 라이브러리는 SQLSTATE 34000 (잘못 된 커서 이름)을 잘못 반환 합니다. **SQLNativeSql** 는 문 준비 또는 실행 시에만 반환 되는 구문 오류를 반환 하기 위한 것이 아닙니다.
