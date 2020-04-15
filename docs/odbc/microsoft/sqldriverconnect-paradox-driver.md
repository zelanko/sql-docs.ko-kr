---
title: SQLDriverConnect (역설 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68171cfab2b65634433b107d829dd2a6e9b5c985
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307114"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 역설 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 **SQLDriverConnect를** 사용하면 DSN(데이터 원본)을 만들지 않고도 드라이버에 연결할 수 있습니다.  
  
 **DSN,** **DBQ**및 **FIL**: 다음 키워드는 모든 드라이버에 대한 연결 문자열에서 지원됩니다.  
  
 **PWD** 키워드도 지원됩니다. PWD 키워드에는 특수 문자를 포함해서는 안 **됩니다(SQLGetInfo** 반환값의 SQL_SPECIAL_CHARACTERS 참조).  
  
 암호로 보호된 파일을 사용자가 연 후에는 다른 사용자가 동일한 파일을 열 수 없습니다.  
  
 다음 표에서는 각 드라이버에 연결하는 데 필요한 최소 키워드를 보여 주며 **SQLDriverConnect**에 사용되는 키워드/값 쌍의 예를 제공합니다. DRIVERID 값의 전체 목록은 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)를 참조하십시오.  
  
> [!NOTE]  
>  역설 드라이버에 대해 DBQ 또는 DefaultDir을 지정하지 않으면 드라이버가 현재 디렉터리에 연결됩니다.  
  
|드라이버|필요한 키워드|예제|  
|------------|-----------------------|-------------|  
|역설|드라이버, 드라이버 ID|드라이버={Microsoft 역설 드라이버(*.db)}; DBQ=c:\temp;드라이버ID=26|
