---
title: datetime 데이터 형식 변환 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4042827c3f4b96344845fea72d479a8de343d133
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705460"
---
# <a name="datetime-data-type-conversions-odbc"></a>datetime 데이터 형식 변환(ODBC)
  다음 변환은 OLE DB에서 이미 정의되었거나 OLE DB의 지속적인 확장에 포함됩니다. 각 공급자가 제공하는 변환은 공급자가 제공하는 커뮤니티에 의해 결정되며, 그 결과 공급자 간에 일치하지 않는 경우가 많습니다. 대괄호 안에 있는 값은 선택적 요소입니다.  
  
-   datetime 문자열의 형식은 'yyyy-mm-dd[ hh:mm:ss[.9999999][ plus/minus hh:mm]]'입니다.  
  
-   시간 문자열의 형식은 'hh:mm:ss[.9999999]'입니다.  
  
-   날짜 문자열의 형식은 'yyyy-mm-dd'입니다.  
  
 문자열에서 변환을 시작하면 공백 및 필드 너비를 보다 융통성 있게 사용할 수 있습니다. 자세한 내용은 [ODBC 날짜 및 시간 향상을 위한 데이터 형식 지원](data-type-support-for-odbc-date-and-time-improvements.md)의 "데이터 형식: 문자열 및 리터럴" 섹션을 참조 하세요.  
  
 일반적인 변환 규칙은 다음과 같습니다.  
  
-   시간 구성 요소가 없지만 받는 사람이 시간을 저장할 수 있는 경우 시간이 0으로 설정됩니다.  
  
-   날짜 구성 요소가 없지만 받는 사람이 날짜를 저장할 수 있는 경우 현재 날짜가 사용됩니다.  
  
-   클라이언트에서 사용하는 데이터 형식에는 표준 시간대 구성 요소가 없지만 서버에서 표준 시간대를 저장할 수 있는 경우 날짜가 클라이언트 표준 시간대로 저장됩니다. 이 동작은 서버 동작과는 다릅니다.  
  
-   서버 유형에는 표준 시간대 구성 요소가 없지만 클라이언트 유형에 표준 시간대 구성 요소가 있는 경우 시간이 서버에 저장되기 전에 UTC로 변환됩니다.  
  
-   시간 구성 요소가 있지만 받는 사람이 시간을 저장할 수 없는 경우 시간 구성 요소가 무시됩니다.  
  
-   날짜 구성 요소가 있지만 받는 사람이 날짜를 저장할 수 없는 경우 날짜 구성 요소가 무시됩니다.  
  
-   C에서 SQL로 변환할 때 초 또는 소수 자릿수 초의 잘림이 발생하는 경우 SQLSTATE 22008 및 "Datetime 필드 오버플로" 메시지가 포함된 진단 레코드가 생성됩니다.  
  
-   SQL에서 C로 변환할 때 초 또는 소수 자릿수 초의 잘림이 발생하는 경우 SQLSTATE 01S07 및 "일부가 잘렸습니다" 메시지가 포함된 진단 레코드가 생성됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [C에서 SQL로의 변환](datetime-data-type-conversions-from-c-to-sql.md)  
 C 형식을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜/시간 형식으로 변환할 때 고려해야 할 문제를 표시합니다.  
  
 [SQL에서 C로 변환](datetime-data-type-conversions-from-sql-to-c.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜/시간 형식을 C 형식으로 변환할 때 고려해야 할 문제를 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;날짜 및 시간 기능 향상](date-and-time-improvements-odbc.md)  
  
  
