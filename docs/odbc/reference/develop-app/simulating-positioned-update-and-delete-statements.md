---
title: 위치 업데이트 및 삭제 문 시뮬레이션 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1eb498a99180d145147e67c8955eeb7a0027024
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301994"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>현재 위치 업데이트 및 Delete 문 시뮬레이션
데이터 원본이 위치 업데이트 및 삭제 문을 지원하지 않는 경우 드라이버는 이를 시뮬레이션할 수 있습니다. 예를 들어 ODBC 커서 라이브러리는 위치 가 있는 업데이트 및 삭제 문을 시뮬레이션합니다. 위치 업데이트 및 삭제 문을 시뮬레이션하는 일반적인 전략은 위치가 있는 문을 검색된 문으로 변환하는 것입니다. 이 작업은 **WHERE CURRENT CURRENT** OF 절을 현재 행을 식별하는 검색된 **WHERE** 절로 대체하여 수행됩니다.  
  
 예를 들어 CustID 열은 Customers 테이블의 각 행을 고유하게 식별하므로 위치 지정 삭제 문이  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 변환될 수 있습니다.  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 드라이버는 **WHERE** 절에서 다음 *행 식별자* 중 하나를 사용할 수 있습니다.  
  
-   값이 테이블의 모든 행을 고유하게 식별하는 역할을 하는 열입니다. 예를 들어 **SQL_BEST_ROWID SQLSpecialColumns를** 호출하면 이 용도에 맞는 최적의 열 또는 열 집합이 반환됩니다.  
  
-   모든 행을 고유하게 식별하기 위해 일부 데이터 원본에서 제공하는 의사 열입니다. **SQLSpecialColumns를**호출하여 검색할 수도 있습니다.  
  
-   사용 가능한 경우 고유한 인덱스입니다.  
  
-   결과 집합의 모든 열입니다.  
  
 드라이버가 생성하는 WHERE 절에서 사용해야 하는 **열은** 드라이버에 따라 다릅니다. 일부 데이터 원본에서 행 식별자를 확인하는 데 많은 비용이 들 수 있습니다. 그러나 실행 속도가 빠르며 시뮬레이션된 문이 최대 한 행에서 업데이트 또는 삭제되도록 보장합니다. 기본 DBMS의 기능에 따라 행 식별자를 사용하는 데 비용이 많이 들 수 있습니다. 그러나 실행 속도가 빠르며 시뮬레이션된 문이 하나의 행만 업데이트하거나 삭제하도록 보장합니다. 결과 집합의 모든 열을 사용하는 옵션은 일반적으로 훨씬 쉽게 설정할 수 있습니다. 그러나 실행 속도가 느리며 열이 행을 고유하게 식별하지 않으면 특히 결과 집합의 선택 목록에 기본 테이블에 있는 모든 열이 포함되지 않은 경우 행이 의도치 않게 업데이트되거나 삭제될 수 있습니다.  
  
 드라이버가 지원하는 이전 전략에 따라 응용 프로그램은 드라이버가 SQL_ATTR_SIMULATE_CURSOR 문 특성과 함께 사용할 전략을 선택할 수 있습니다. 응용 프로그램이 실수로 행을 업데이트하거나 삭제하는 위험을 감수하는 것은 이상하게 보일 수 있지만 응용 프로그램은 결과 집합의 열이 결과 집합의 각 행을 고유하게 식별하도록 하여 이 위험을 제거할 수 있습니다. 이렇게 하면 드라이버가 이 작업을 수행할 필요가 없습니다.  
  
 드라이버가 행 식별자를 사용하도록 선택하면 결과 집합을 만드는 **UPDATEFOR SELECT** 문을 가로채게 됩니다. 선택 목록의 열이 행을 효과적으로 식별하지 못하면 드라이버는 선택 목록의 끝에 필요한 열을 추가합니다. 일부 데이터 원본에는 오라클의 ROWID 열과 같이 행을 항상 고유하게 식별하는 단일 열이 있습니다. 이러한 열을 사용할 수 있는 경우 드라이버는 이를 사용합니다. 그렇지 않으면 드라이버는 **FROM** 절의 각 테이블에 대해 **SQLSpecialColumns를** 호출하여 각 행을 고유하게 식별하는 열 목록을 검색합니다. 이 기법에서 발생하는 일반적인 제한 사항은 **FROM** 절에 두 개 이상의 테이블이 있는 경우 커서 시뮬레이션에 실패한다는 것입니다.  
  
 드라이버가 행을 식별하는 방법에 관계없이 일반적으로 데이터 원본으로 보내기 전에 **SELECT FOR UPDATE** 문에서 FOR **UPDATE** 절을 제거합니다. **FOR UPDATE OF** 절은 위치 가 있는 업데이트 및 삭제 문에서만 사용됩니다. 위치 업데이트 및 삭제 문을 지원하지 않는 데이터 원본은 일반적으로 지원하지 않습니다.  
  
 응용 프로그램이 실행을 위해 위치 된 업데이트 또는 삭제 문을 제출하는 경우 드라이버는 **WHERE CURRENT OF** 절을 행 식별자를 포함하는 **WHERE** 절로 바꿉니다. 이러한 열의 값은 **WHERE** 절에서 사용하는 각 열에 대해 드라이버가 유지 관리하는 캐시에서 검색됩니다. 드라이버가 **WHERE** 절을 대체한 후 실행을 위해 데이터 원본으로 문을 보냅니다.  
  
 예를 들어 응용 프로그램이 다음 문을 제출하여 결과 집합을 만듭니다.  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 응용 프로그램이 고유성 보장을 요청하는 SQL_ATTR_SIMULATE_CURSOR 설정하고 데이터 원본이 항상 고유하게 행을 식별하는 의사 열을 제공하지 않는 경우 드라이버는 고객 테이블에 대해 **SQLSpecialColumns를** 호출하고 CustID가 고객 테이블의 키임을 발견하고 이를 선택 목록에 추가하고 **FOR UPDATE OF** 절을 제거합니다.  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 응용 프로그램이 고유성 보장을 요청하지 않은 경우 드라이버는 **FOR UPDATE** OF 절만 제거합니다.  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 응용 프로그램이 결과 집합을 스크롤하고 Cust가 결과 집합에 대한 커서의 이름인 다음 위치 업데이트 문을 실행하기 위해 제출한다고 가정합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 응용 프로그램이 고유성 보장을 요청하지 않은 경우 드라이버는 **WHERE** 절을 대체하고 CustID 매개 변수를 캐시의 변수에 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 응용 프로그램이 고유성 보장을 요청하지 않은 경우 드라이버는 **WHERE** 절을 대체하고 이 절의 이름, 주소 및 전화 매개 변수를 캐시의 변수에 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
