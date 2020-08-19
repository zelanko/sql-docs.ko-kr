---
description: SQLDriverConnect(Paradox 드라이버)
title: SQLDriverConnect (Paradox 드라이버) | Microsoft Docs
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
ms.openlocfilehash: 8b6bffe650bfc204660d7345b1bd5a051105fb5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421817"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 **SQLDriverConnect** 를 사용 하면 DSN (데이터 원본)을 만들지 않고도 드라이버에 연결할 수 있습니다.  
  
 모든 드라이버에 대 한 연결 문자열에서 지원 되는 키워드는 **DSN**, **Dbq**및 **FIL**입니다.  
  
 또한 **PWD** 키워드가 지원 됩니다. PWD 키워드는 특수 문자를 포함할 수 없습니다 ( **SQLGetInfo** 반환 값의 SQL_SPECIAL_CHARACTERS 참조).  
  
 사용자가 암호로 보호 된 파일을 연 후에는 다른 사용자가 동일한 파일을 열 수 없습니다.  
  
 다음 표에서는 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 주며, **SQLDriverConnect**에 사용 되는 키워드/값 쌍의 예를 제공 합니다. DRIVERID 값의 전체 목록은 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)를 참조 하세요.  
  
> [!NOTE]  
>  Paradox 드라이버에 대해 DBQ 또는 DefaultDir를 지정 하지 않으면 드라이버가 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예제|  
|------------|-----------------------|-------------|  
|Paradox|드라이버, DriverID|Driver = {Microsoft Paradox Driver (* db-library)}; DBQ = c:\temp; DriverID = 26|
