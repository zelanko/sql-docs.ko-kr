---
title: SQL드라이버커넥트(액세스 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a679cbb16ece3f239b1d17daabc8a294b808287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302914"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 **SQLDriverConnect를** 사용하면 DSN(데이터 원본)을 만들지 않고도 드라이버에 연결할 수 있습니다.  
  
 **DSN,** **DBQ**및 **FIL**: 다음 키워드는 모든 드라이버에 대한 연결 문자열에서 지원됩니다.  
  
 **UID** 및 **PWD** 키워드도 지원됩니다.  
  
 PWD 키워드에는 특수 문자를 포함해서는 안 **됩니다(SQLGetInfo** 반환값의 SQL_SPECIAL_CHARACTERS 참조).  
  
 다음 표에서는 각 드라이버에 연결하는 데 필요한 최소 키워드를 보여 주며 **SQLDriverConnect**에 사용되는 키워드/값 쌍의 예를 제공합니다. DRIVERID 값의 전체 목록은 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)를 참조하십시오.  
  
|드라이버|필요한 키워드|예|  
|------------|-----------------------|--------------|  
|Microsoft Access|드라이버, DBQ|드라이버={Microsoft 액세스 드라이버(*.mdb)}; DBQ=c:\\\temp\\\sample.mdb|
