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
ms.openlocfilehash: 44e9d92c7371451d6bfdd2e1513c3f8fdac8447b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129995"
---
# <a name="descriptor-transitions"></a>설명자 전환
ODBC 설명자에는 다음과 같은 세 가지 상태가 있습니다.  
  
|시스템 상태|Description|  
|-----------|-----------------|  
|D0|할당 되지 않은 설명자|  
|D1i|암시적으로 할당 된 설명자|  
|D1e|명시적으로 할당 된 설명자|  
  
 다음 표에서는 각 ODBC 함수가 설명자 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] *HandleType* 가 SQL_HANDLE_STMT 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DESC 된 경우이 행은 전환을 표시 합니다.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|항목|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|항목 sr-2|(HY017)|D0|  
  
 [1] *HandleType* 가 SQL_HANDLE_STMT 된 경우이 행은 전환을 표시 합니다.  
  
 [2] *HandleType* 가 SQL_HANDLE_DESC 된 경우이 행은 전환을 표시 합니다.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 및 SQLGetDescRec  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|항목|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 및 SQLSetDescRec  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|항목 비슷합니다|--|--|  
  
 [1]이 행은 *DescriptorHandle* 가 IPD, Apd 또는 SQLSetDescField의 핸들 일 때 전환을 표시 하거나 *DescriptorHandle* IRD FieldIdentifier 및 ** 가 SQL_DESC_ARRAY_STATUS_PTR 또는 SQL_DESC_ROWS_PROCESSED_PTR 된 경우 ( **** 의 경우)를 표시 합니다.  
  
## <a name="all-other-odbc-functions"></a>기타 모든 ODBC 함수  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--|--|--|
