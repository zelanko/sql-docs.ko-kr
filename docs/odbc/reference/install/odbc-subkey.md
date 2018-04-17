---
title: ODBC 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a78553cbf67f4056ac50db78b0249189f2e27f26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-subkey"></a>ODBC 하위 키
ODBC 하위 키 아래의 값 ODBC 추적 옵션을 지정합니다. 이 옵션이 설정 하 여 표시 된 ODBC 데이터 원본 관리자 대화 상자의 추적 탭을 통해 **SQLManageDataSources**합니다. ODBC 하위 키 자체는 선택 사항입니다. 다음 표에 나와 있는 것 처럼 이러한 값의 형식은입니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|추적|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*tracefile 경로*|  
  
 값을 다음 표에 설명 된 의미가 있습니다.  
  
|Value|의미|  
|-----------|-------------|  
|추적|경우에 1로 응용 프로그램 호출 추적 값은 설정 되 면 **SQLAllocHandle** SQL_HANDLE_ENV 옵션으로 추적을 호출 응용 프로그램에 대해 사용할 수 있습니다.<br /><br /> 응용 프로그램이 호출 하는 경우 추적 키워드 0으로 설정 되어 **SQLAllocHandle** SQL_HANDLE_ENV 옵션으로 추적 호출 응용 프로그램에 대해 사용할 수 없습니다. 이 값은 기본값입니다.<br /><br /> 응용 프로그램을 사용 하도록 설정 하거나 SQL_ATTR_TRACE 연결 특성을 사용 하 여 추적을 사용 하지 않도록 설정할 수 있습니다. 그러나 이렇게 하면 하므로 변경 되지 않습니다이 값에 대 한 데이터.|  
|TraceFile|추적을 사용 하는 경우 드라이버 관리자 TraceFile 값으로 지정 된 추적 파일에 씁니다.<br /><br /> 지정 된 추적 파일이 없는 경우 드라이버 관리자는 현재 드라이브에서 Sql.log 파일에 씁니다. 이 값은 기본값입니다.<br /><br /> 단일 응용 프로그램에 대 한 추적을 사용할지 또는 각 응용 프로그램에 다른 추적 파일을 지정 해야 합니다. 그렇지 않은 경우 둘 이상의 응용 프로그램은 하려고 이와 동시에 동일한 추적 파일을 열 때문에 오류가 발생 합니다.<br /><br /> 응용 프로그램 SQL_ATTR_TRACEFILE 연결 특성으로 새 추적 파일을 지정할 수 있습니다. 그러나 이렇게 하면 하므로 변경 되지 않습니다이 값에 대 한 데이터.|  
  
 예를 들어 추적을 사용 하 고 추적 파일은 C:\Odbc.log 가정 합니다. ODBC 하위 키 아래에 값은 다음과 같이 합니다.  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
