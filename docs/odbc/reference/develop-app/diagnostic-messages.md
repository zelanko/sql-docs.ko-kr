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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be63e9d78960e40ac5e9ee016d2cfd868d99a922
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305834"
---
# <a name="diagnostic-messages"></a>진단 메시지
각 SQLSTATE와 함께 진단 메시지가 반환 됩니다. 여러 메시지와 함께 동일한 SQLSTATE가 반환 되는 경우가 많습니다. 예를 들어 SQL 구문에서 대부분의 오류에 대해 SQLSTATE 42000 (구문 오류 또는 액세스 위반)이 반환 됩니다. 그러나 각 구문 오류는 다른 메시지로 설명할 수 있습니다.  
  
 샘플 진단 메시지는 부록 A 및 각 함수의 SQLSTATEs 테이블의 Error 열에 나열 됩니다. 드라이버가 이러한 메시지를 반환할 수 있지만 데이터 원본에 의해 전달 되는 모든 메시지를 반환할 가능성이 높습니다.  
  
 응용 프로그램은 일반적으로 SQLSTATE 및 원시 오류 코드와 함께 진단 메시지를 사용자에 게 표시 합니다. 이렇게 하면 사용자 및 지원 담당자가 문제의 원인을 확인할 수 있습니다. 메시지에 포함 된 구성 요소 정보는이 작업을 수행 하는 데 특히 유용 합니다.  
  
 진단 메시지는 드라이버, 게이트웨이 및 드라이버 관리자와 같은 ODBC 연결의 데이터 원본 및 구성 요소에서 제공 됩니다. 일반적으로 데이터 원본은 ODBC를 직접 지원 하지 않습니다. 따라서 ODBC 연결의 구성 요소가 데이터 원본에서 메시지를 수신 하는 경우 데이터 원본을 메시지의 원본으로 식별 해야 합니다. 또한 메시지를 받은 구성 요소로도 식별 해야 합니다.  
  
 오류 또는 경고의 소스가 구성 요소 자체인 경우 진단 메시지에서이를 설명 해야 합니다. 따라서 메시지의 텍스트에는 두 가지 형식이 있습니다. 데이터 원본에서 발생 하지 않는 오류 및 경고의 경우 진단 메시지는 다음 형식을 사용 해야 합니다.  
  
 **[** *공급 업체-식별자* **] [** *ODBC-구성 요소-식별자* **]** *구성 요소 제공 텍스트*  
  
 데이터 원본에서 발생 하는 오류 및 경고의 경우 진단 메시지는 다음 형식을 사용 해야 합니다.  
  
 **[** *공급 업체-식별자* **] [** *ODBC-구성 요소-식별자* **] [** *데이터 원본-식별자* **]** *데이터 원본 제공 텍스트*  
  
 다음 표에서는 각 요소의 의미를 보여 줍니다.  
  
|요소|의미|  
|-------------|-------------|  
|*공급 업체-식별자*|오류나 경고가 발생 했거나 데이터 원본에서 직접 오류나 경고를 받은 구성 요소의 공급 업체를 식별 합니다.|  
|*ODBC-구성 요소-식별자*|오류나 경고가 발생 했거나 데이터 원본에서 직접 오류나 경고를 받은 구성 요소를 식별 합니다.|  
|*데이터 원본-식별자*|데이터 원본을 식별 합니다. 파일 기반 드라이버의 경우 일반적으로 DBMS 기반 드라이버에 대 한 Xbase [1]과 같은 파일 형식이 며 DBMS 제품입니다.|  
|*구성 요소 제공 텍스트*|ODBC 구성 요소에 의해 생성 됩니다.|  
|*데이터 원본 제공 텍스트*|데이터 원본에 의해 생성 됩니다.|  
  
 [1]이 경우 드라이버는 드라이버와 데이터 원본 모두로 작동 합니다.  
  
 대괄호 (**[]**)는 메시지에 포함 되어야 하며 선택적 항목을 나타내지는 않습니다.
