---
description: 현재 위치 업데이트 및 Delete 문 시뮬레이션
title: 위치 지정 업데이트 및 Delete 문 시뮬레이션 | Microsoft Docs
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
ms.openlocfilehash: 06f6faad1b5b6cb83616575ea8732cac98b88ed0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499816"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>현재 위치 업데이트 및 Delete 문 시뮬레이션
데이터 원본에서 위치 지정 update 및 delete 문을 지원 하지 않는 경우 드라이버에서 이러한 문을 시뮬레이트할 수 있습니다. 예를 들어 ODBC 커서 라이브러리는 위치 지정 update 및 delete 문을 시뮬레이트합니다. 위치 지정 update 및 delete 문을 시뮬레이트하는 일반적인 전략은 위치 지정 문을 검색 된 문으로 변환 하는 것입니다. **WHERE CURRENT OF** 절을 현재 행을 식별 하는 검색 된 **where** 절로 바꿔서이 작업을 수행 합니다.  
  
 예를 들어 CustID 열은 Customers 테이블의 각 행을 고유 하 게 식별 하기 때문에 배치 된 delete 문이  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 로 변환 될 수 있습니다.  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 드라이버는 **WHERE** 절에서 다음 *행 식별자* 중 하나를 사용할 수 있습니다.  
  
-   테이블의 모든 행을 고유 하 게 식별 하는 값을 갖는 열입니다. 예를 들어 SQL_BEST_ROWID를 사용 하 여 **SQLSpecialColumns** 를 호출 하면이 용도를 제공 하는 최적의 열 또는 열 집합을 반환 합니다.  
  
-   모든 행을 고유 하 게 식별 하기 위해 일부 데이터 원본에서 제공 하는 의사 (Pseudo) 열 **SQLSpecialColumns**를 호출 하 여 검색할 수도 있습니다.  
  
-   사용할 수 있는 경우 고유 인덱스입니다.  
  
-   결과 집합의 모든 열입니다.  
  
 드라이버가 생성 하는 **where** 절에서 드라이버가 사용 해야 하는 열은 드라이버에 따라 달라 집니다. 일부 데이터 원본에서 행 식별자를 확인 하는 것은 비용이 많이 들 수 있습니다. 그러나 시뮬레이션 된 문이 최대 하나의 행을 업데이트 하거나 삭제 하는 것이 더 빠릅니다. 기본 DBMS의 기능에 따라 행 식별자를 설정 하는 데 비용이 많이 들 수 있습니다. 그러나 실행 하는 것이 더 빠르며 시뮬레이션 된 문이 하나의 행만 업데이트 하거나 삭제 하도록 보장 합니다. 일반적으로 결과 집합의 모든 열을 사용 하는 옵션을 설정 하는 것이 훨씬 쉽습니다. 그러나 실행 하는 속도가 느려지고 열이 행을 고유 하 게 식별 하지 않으면 특히 결과 집합에 대 한 select 목록에 기본 테이블에 있는 모든 열이 포함 되어 있지 않은 경우에는 행이 실수로 업데이트 되거나 삭제 될 수 있습니다.  
  
 드라이버에서 지원 되는 위의 전략에 따라 응용 프로그램에서 SQL_ATTR_SIMULATE_CURSOR statement 특성에 사용할 드라이버를 원하는 전략을 선택할 수 있습니다. 응용 프로그램에서 행을 실수로 업데이트 하거나 삭제 하지 못할 수 있지만 응용 프로그램은 결과 집합의 열이 결과 집합의 각 행을 고유 하 게 식별 하도록 하 여이 위험을 제거할 수 있습니다. 이렇게 하면 드라이버를 저장 하 여이 작업을 수행 해야 합니다.  
  
 드라이버에서 행 식별자를 사용 하도록 선택 하는 경우 결과 집합을 만드는 **SELECT FOR UPDATE** 문을 가로챕니다. Select 목록의 열에서 행을 효율적으로 식별 하지 못하는 경우에는 필요한 열이 선택 목록의 끝에 추가 됩니다. 일부 데이터 원본에는 Oracle의 ROWID 열과 같이 항상 행을 고유 하 게 식별 하는 단일 열이 있습니다. 이러한 열을 사용할 수 있는 경우 드라이버는이를 사용 합니다. 그렇지 않으면 드라이버는 **from** 절의 각 테이블에 대해 **SQLSpecialColumns** 를 호출 하 여 각 행을 고유 하 게 식별 하는 열 목록을 검색 합니다. 이 기술로 인해 발생 하는 일반적인 제한 사항은 **from** 절에 테이블이 두 개 이상 있을 경우 커서 시뮬레이션이 실패 한다는 것입니다.  
  
 드라이버에서 행을 식별 하는 방법에 관계 없이 일반적으로 데이터 원본으로 보내기 전에 **SELECT FOR update** 문에 **대해 for update** 절을 제거 합니다. **FOR update** 절은 위치 지정 update 및 delete 문에만 사용 됩니다. 위치 지정 update 및 delete 문을 지원 하지 않는 데이터 원본은 일반적으로이를 지원 하지 않습니다.  
  
 응용 프로그램이 실행을 위해 배치 된 update 또는 delete 문을 제출할 때 드라이버는 **WHERE CURRENT OF** 절을 행 식별자를 포함 하는 **where** 절로 바꿉니다. 이러한 열의 값은 **where** 절에서 사용 하는 각 열에 대해 드라이버에 의해 유지 관리 되는 캐시에서 검색 됩니다. 드라이버가 **WHERE** 절을 대체 한 후에는 실행을 위해 문을 데이터 원본으로 보냅니다.  
  
 예를 들어 응용 프로그램에서 다음 문을 전송 하 여 결과 집합을 만드는 경우를 가정 합니다.  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 응용 프로그램에서 고유성 보장을 요청 하도록 SQL_ATTR_SIMULATE_CURSOR를 설정 하 고 데이터 원본에서 항상 행을 고유 하 게 식별 하는 의사 (pseudo) 열을 제공 하지 않는 경우 드라이버는 Customers 테이블에 대해 **SQLSpecialColumns** 를 호출 하 고 CustID가 customers 테이블의 키인 것을 검색 한 다음 select 목록에 추가 하 고 **for UPDATE of** 절을 제거 합니다.  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 응용 프로그램에서 고유성 보장을 요청 하지 않은 경우 드라이버는 **FOR UPDATE** 절만 제거 합니다.  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 응용 프로그램이 결과 집합을 스크롤하여 실행을 위해 다음 위치에 배치 된 update 문을 제출 한다고 가정 합니다. 여기서 Cust는 결과 집합에 대 한 커서의 이름입니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 응용 프로그램에서 고유성이 보장을 요청 하지 않은 경우 드라이버는 **WHERE** 절을 대체 하 고 CustID 매개 변수를 캐시의 변수에 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 응용 프로그램에서 고유성이 보장 되지 않는 경우 드라이버는 **WHERE** 절을 대체 하 고이 절의 Name, Address 및 Phone 매개 변수를 해당 캐시의 변수에 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
