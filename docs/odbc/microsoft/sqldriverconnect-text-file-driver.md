---
description: SQLDriverConnect(텍스트 파일 드라이버)
title: SQLDriverConnect (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2eb5c35e9f6ae56caa3c6e4ca7473defe3b8bc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421807"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 **SQLDriverConnect** 를 사용 하면 DSN (데이터 원본)을 만들지 않고도 드라이버에 연결할 수 있습니다.  
  
 모든 드라이버에 대 한 연결 문자열에서 지원 되는 키워드는 **DSN**, **Dbq**및 **FIL**입니다.  
  
 다음 표에서는 각 드라이버에 연결 하는 데 필요한 최소 키워드를 보여 주며, **SQLDriverConnect**에 사용 되는 키워드/값 쌍의 예를 제공 합니다. DRIVERID 값의 전체 목록은 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)를 참조 하세요.  
  
> [!NOTE]  
>  텍스트 드라이버에 DBQ 또는 DefaultDir를 지정 하지 않으면 드라이버가 현재 디렉터리에 연결 됩니다.  
  
|드라이버|필요한 키워드|예제|  
|------------|-----------------------|--------------|  
|텍스트|드라이버|Driver = {Microsoft 텍스트 드라이버 (* .txt;) \* . csv)}; DefaultDir = c:\temp|
