---
title: ODBC 서브키 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287443"
---
# <a name="odbc-subkey"></a>ODBC 하위 키
ODBC 하위 키 아래의 값은 ODBC 추적 옵션을 지정합니다. 이러한 옵션은 **SQLManageDataSource**에 의해 표시되는 ODBC 데이터 원본 관리자 대화 상자의 추적 탭을 통해 설정됩니다. ODBC 하위 키 자체는 선택 사항입니다. 이러한 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|추적|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*추적 파일 경로*|  
  
 값에는 다음 표에 설명된 의미가 있습니다.  
  
|값|의미|  
|-----------|-------------|  
|추적|응용 프로그램이 SQL_HANDLE_ENV 옵션으로 **SQLAllocHandle을** 호출할 때 추적 값이 1로 설정된 경우 호출 응용 프로그램에 대해 추적이 활성화됩니다.<br /><br /> 응용 프로그램에서 SQL_HANDLE_ENV 옵션으로 **SQLAllocHandle을** 호출할 때 추적 키워드가 0으로 설정된 경우 호출 응용 프로그램에 대해 추적이 비활성화됩니다. 기본값입니다.<br /><br /> 응용 프로그램은 SQL_ATTR_TRACE 연결 특성을 사용하여 추적을 활성화하거나 비활성화할 수 있습니다. 그러나 이렇게 해도 이 값에 대한 데이터는 변경되지 않습니다.|  
|TraceFile|추적을 사용하도록 설정하면 드라이버 관리자는 TraceFile 값에 의해 지정된 추적 파일에 기록합니다.<br /><br /> 추적 파일을 지정하지 않으면 드라이버 관리자가 현재 드라이브의 Sql.log 파일에 기록합니다. 기본값입니다.<br /><br /> 추적은 단일 응용 프로그램에만 사용하거나 각 응용 프로그램은 다른 추적 파일을 지정해야 합니다. 그렇지 않으면 둘 이상의 응용 프로그램이 동시에 동일한 추적 파일을 열려고 시도하여 오류가 발생합니다.<br /><br /> 응용 프로그램은 SQL_ATTR_TRACEFILE 연결 특성이 있는 새 추적 파일을 지정할 수 있습니다. 그러나 이렇게 해도 이 값에 대한 데이터는 변경되지 않습니다.|  
  
 예를 들어 추적이 활성화되어 있고 추적 파일이 C:\Odbc.log라고 가정합니다. ODBC 하위 키 아래의 값은 다음과 같습니다.  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
