---
title: ODBC 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96e9a5f4c3cdac5097686528d3c089d9ec5826f7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287443"
---
# <a name="odbc-subkey"></a>ODBC 하위 키
ODBC 하위 키 아래의 값은 ODBC 추적 옵션을 지정 합니다. 이러한 옵션은 **SQLManageDataSources**에서 표시 하는 ODBC 데이터 원본 관리자 대화 상자의 추적 탭을 통해 설정 됩니다. ODBC 하위 키 자체는 선택 사항입니다. 이러한 값의 형식은 다음 표에 나와 있습니다.  
  
|Name|데이터 형식|데이터|  
|----------|---------------|----------|  
|추적|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile-path*|  
  
 값의 의미는 다음 표에 설명 되어 있습니다.  
  
|값|의미|  
|-----------|-------------|  
|추적|응용 프로그램이 SQL_HANDLE_ENV 옵션을 사용 하 여 **SQLAllocHandle** 를 호출할 때 추적 값이 1로 설정 된 경우에는 호출 응용 프로그램에 대해 추적을 사용할 수 있습니다.<br /><br /> 응용 프로그램이 SQL_HANDLE_ENV 옵션을 사용 하 여 **SQLAllocHandle** 를 호출할 때 Trace 키워드가 0으로 설정 되 면 호출 응용 프로그램에 대해 추적을 사용할 수 없습니다. 기본값입니다.<br /><br /> 응용 프로그램은 SQL_ATTR_TRACE 연결 특성을 사용 하 여 추적을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 그러나 이렇게 하면이 값에 대 한 데이터가 변경 되지 않습니다.|  
|TraceFile|추적을 사용 하는 경우 드라이버 관리자는 TraceFile 값으로 지정 된 추적 파일에 기록 합니다.<br /><br /> 추적 파일을 지정 하지 않으면 드라이버 관리자는 현재 드라이브의 Sql .log 파일에 기록 합니다. 기본값입니다.<br /><br /> 추적은 단일 응용 프로그램에만 사용 해야 합니다. 또는 각 응용 프로그램은 다른 추적 파일을 지정 해야 합니다. 그렇지 않으면 둘 이상의 응용 프로그램이 동시에 같은 추적 파일을 열려고 시도 하므로 오류가 발생 합니다.<br /><br /> 응용 프로그램은 SQL_ATTR_TRACEFILE 연결 특성을 사용 하 여 새 추적 파일을 지정할 수 있습니다. 그러나 이렇게 하면이 값에 대 한 데이터가 변경 되지 않습니다.|  
  
 예를 들어 추적을 사용 하도록 설정 하 고 추적 파일을 C:\Odbc.log. ODBC 하위 키 아래에 있는 값은 다음과 같습니다.  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
