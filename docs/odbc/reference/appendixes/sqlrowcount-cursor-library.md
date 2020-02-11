---
title: SQLRowCount (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be902866cfcf98a10af2c3741926de8b7541bb79
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125605"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **Sqlrowcount** 함수를 사용 하는 방법을 설명 합니다. **Sqlrowcount**에 대 한 일반 정보는 [sqlrowcount 함수](../../../odbc/reference/syntax/sqlrowcount-function.md)를 참조 하세요.  
  
 응용 프로그램에서 커서와 연결 된 문을 사용 하 여 **Sqlrowcount** 를 호출 하면 커서 라이브러리는 드라이버에서 검색 한 데이터 행 수를 반환 합니다.  
  
 응용 프로그램에서 위치 지정 update 또는 delete 문과 연결 된 문을 사용 하 여 **Sqlrowcount** 를 호출 하면 커서 라이브러리는 문의 영향을 받는 행 수를 반환 합니다.  
  
 **SELECT** 문 다음에 응용 프로그램에서 **sqlrowcount** 를 호출 하면 커서 라이브러리는-1을 반환 합니다.
