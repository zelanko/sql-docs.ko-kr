---
title: 진단 메시지 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 883cd29d8628f1e9270ae95a772c4d116b896710
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767631"
---
# <a name="diagnostic-messages"></a>진단 메시지
진단 메시지를 각 SQLSTATE를 사용 하 여 반환 됩니다. 동일한 SQLSTATE는 서로 다른 메시지의 수를 사용 하 여 자주 반환 됩니다. 예를 들어, SQLSTATE 42000 (구문 오류 또는 액세스 위반)는 SQL 구문에서 대부분의 오류에 대 한 반환 됩니다. 그러나 각 구문 오류는 다른 메시지를 설명할 수 가능성이 높습니다.  
  
 샘플 진단 메시지 SQLSTATEs 각 함수에 부록 A의 테이블에 있는 Error 열에 나열 됩니다. 드라이버는 이러한 메시지를 반환할 수 있지만 데이터 원본에서 모든 메시지에 전달 되는 반환 됩니다.  
  
 응용 프로그램은 일반적으로 SQLSTATE 및 원시 오류 코드와 함께 사용자에 게 진단 메시지를 표시 합니다. 이렇게 하면 사용자 및 고객 지원 담당자에 문제의 원인을 확인 합니다. 메시지에 포함 된 구성 요소 정보를이 작업을 수행할 때 특히 유용 합니다.  
  
 진단 메시지 데이터 원본과 ODBC 연결에서 드라이버, 게이트웨이 및 드라이버 관리자와 같은 구성 요소에서 제공 됩니다. 일반적으로 데이터 원본은 ODBC을 직접 지원 하지 않습니다. 결과적으로 ODBC 연결의 구성 요소에서 데이터 원본에서 메시지를 수신 하는 경우 데이터 원본 메시지의 원본으로 식별 해야 합니다. 메시지를 수신 하는 구성 요소와 자체 식별도 해야 합니다.  
  
 오류 또는 경고의 원본 구성 요소 자체가 이면 진단 메시지 설명 해야 합니다. 따라서 메시지의 텍스트에는 두 가지 형식입니다. 진단 메시지는 오류 및 경고 데이터 원본에서 발생 하지 않는 경우이 형식을 사용 해야 합니다.  
  
 **[** *공급 업체 식별자* **] [** *ODBC 구성 요소 식별자* **]** *구성 요소-제공 된 텍스트*  
  
 데이터 원본에서 발생 하는 경고와 오류에 대 한 진단 메시지는이 형식을 사용 해야 합니다.  
  
 **[** *공급 업체 식별자* **] [** *ODBC 구성 요소 식별자* **] [** *데이터 원본 id*  **]** *데이터-소스 제공-텍스트*  
  
 다음 표에서 각 요소의 의미를 보여 줍니다.  
  
|요소|의미|  
|-------------|-------------|  
|*공급 업체 id*|오류 또는 경고가 발생 하거나 데이터 원본에서 직접 오류 또는 경고를 수신 하는 구성 요소의 공급 업체를 식별 합니다.|  
|*ODBC 구성 요소 id*|오류 또는 경고가 발생 하거나 데이터 원본에서 직접 오류 또는 경고를 수신 하는 구성 요소를 식별 합니다.|  
|*데이터 원본 id*|데이터 소스를 식별합니다. 파일 기반 드라이버에 대 한이 일반적으로 파일 형식, Xbase [1]에 대 한 DBMS 기반 드라이버와 같은 DBMS 제품입니다.|  
|*구성 요소-제공 된 텍스트*|ODBC 구성 요소에 의해 생성 됩니다.|  
|*데이터 원본-제공-텍스트*|데이터 원본에서 생성 합니다.|  
  
 [1]이 경우 드라이버 역할을 하는 드라이버 및 데이터 원본입니다.  
  
 대괄호 (**[]**) 메시지에 포함 되어야 하며 선택적 항목을 나타내지 않습니다.
