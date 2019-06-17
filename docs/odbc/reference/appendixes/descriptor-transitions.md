---
title: 설명자 전환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 027b711c5c1a2cb2d35e65efdc2b00f441841d8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240975"
---
# <a name="descriptor-transitions"></a>설명자 전환
ODBC 설명자는 다음 세 가지 상태입니다.  
  
|State|Description|  
|-----------|-----------------|  
|D0|할당 되지 않은 설명자|  
|D1i|암시적으로 할당 된 설명자|  
|D1e|명시적으로 할당 된 설명자|  
  
 다음 표에 각 ODBC 함수 설명자 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적 방법|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e[2]|--|--|  
  
 [1]이이 행 표시 전환 때 *HandleType* 호출 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DESC 되었습니다.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적 방법|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적 방법|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)[2]|(HY017)|D0|  
  
 [1]이이 행 표시 전환 때 *HandleType* 호출 되었습니다.  
  
 [2]이이 행 표시 전환 때 *HandleType* SQL_HANDLE_DESC 되었습니다.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 및 SQLGetDescRec  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적 방법|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 및 SQLSetDescRec  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적 방법|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)[1]|--|--|  
  
 [1]이이 행은 전환을 보여 줍니다. 때 *DescriptorHandle* 된 카드가, APD, 또는 IPD, 핸들 또는 (에 대 한 **SQLSetDescField**) 때 *DescriptorHandle* IRD의 핸들을 되었습니다 및 *FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR 되었거나 SQL_DESC_ROWS_PROCESSED_PTR 합니다.  
  
## <a name="all-other-odbc-functions"></a>다른 모든 ODBC 함수  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적 방법|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--|--|--|
