---
title: 문 매개 변수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 74cd70bcd9107d68551dc3f82eb1e01f76a549b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297904"
---
# <a name="using-statement-parameters"></a>문 매개 변수 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  매개 변수는 ODBC 애플리케이션에서 다음을 수행할 수 있도록 하는 SQL 문의 변수입니다.  
  
-   효율적으로 테이블의 열 값을 제공합니다.  
  
-   쿼리 조건을 생성하여 사용자 상호 작용을 향상시킵니다.  
  
-   **Text**, **ntext**및 **image** 데이터와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]관련 C 데이터 형식을 관리 합니다.  
  
 예를 들어 **부품** 테이블에는 **PartID**, **설명**및 **가격**이라는 열이 있습니다. 매개 변수 없이 부품을 추가하려면 다음과 같이 SQL 문을 생성해야 합니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 알려진 값 집합이 포함된 행 하나를 삽입하는 경우 이 문을 사용해도 되지만 애플리케이션에서 여러 행을 삽입해야 하는 경우에는 비효율적입니다. ODBC는 애플리케이션에서 매개 변수 표식을 통해 SQL 문의 모든 데이터 값을 바꿀 수 있도록 하여 이 문제를 해결합니다. 이 경우 물음표(?)가 표시됩니다. 다음 예에서는 3개의 데이터 값이 매개 변수 표식으로 바뀝니다.  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 그런 다음 매개 변수 표식이 애플리케이션 변수에 바인딩됩니다. 새 행을 삽입하려면 애플리케이션에서 변수 값을 설정하고 문을 실행하기만 하면 됩니다. 그런 다음 드라이버가 변수의 현재 값을 검색하여 데이터 원본에 보냅니다. 문이 여러 번 실행되는 경우 애플리케이션에서 문을 준비하여 프로세스를 훨씬 효율적으로 만들 수 있습니다.  
  
 각 매개 변수 표식은 왼쪽에서 오른쪽으로 매개 변수에 할당되는 서수 번호로 참조됩니다. SQL 문에서 맨 왼쪽에 있는 매개 변수 표식의 서수 값은 1이고, 다음 표식의 서수 값은 2입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [매개 변수 바인딩](../../relational-databases/native-client-odbc-queries/using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;쿼리 실행](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
