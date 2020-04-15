---
title: 설명자 전환 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec5c26bdde8a0d470f2d93e753504bf1c51edcc0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307044"
---
# <a name="descriptor-transitions"></a>설명자 전환
ODBC 설명자는 다음과 같은 세 가지 상태를 갖습니다.  
  
|시스템 상태|설명|  
|-----------|-----------------|  
|D0|할당되지 않은 설명자|  
|D1i|암시적으로 할당된 설명자|  
|D1e|명시적으로 할당된 설명자|  
  
 다음 표는 각 ODBC 함수가 설명자 상태에 미치는 영향을 보여 줍니다.  
  
## <a name="sqlallochandle"></a>SQLAlloc핸들  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e[2]|--|--|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_STMT 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_DESC 때의 전환을 보여 주었습니다.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH) [2]|(HY017)|D0|  
  
 [1] 이 행은 *핸들타입이* SQL_HANDLE_STMT 때의 전환을 보여 주었습니다.  
  
 [2] 이 행은 *핸들타입이* SQL_HANDLE_DESC 때의 전환을 보여 주었습니다.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDesc필드 및 SQLGetDescRec  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDesc필드 및 SQLSetDescRec  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|(IH) [1]|--|--|  
  
 [1] 이 행은 *설명자핸들이* ARD, APD 또는 IPD의 핸들이거나(SQLSetDescField의 경우) *설명자핸들이* IRD의 핸들이 SQL_DESC_ARRAY_STATUS_PTR었거나 SQL_DESC_ROWS_PROCESSED_PTR 때의 전환을 보여 SQL_DESC_ROWS_PROCESSED_PTR. **SQLSetDescField** *FieldIdentifier*  
  
## <a name="all-other-odbc-functions"></a>기타 모든 ODBC 함수  
  
|D0<br /><br /> 할당되지 않음|D1i<br /><br /> 암시적|D1e<br /><br /> Explicit|  
|------------------------|----------------------|----------------------|  
|--|--|--|
