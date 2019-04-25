---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d98d40ae24c68f90a304edb0293febfe76fac2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445895"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>현재 위치 업데이트 및 Delete 문 시뮬레이션
데이터 원본 위치 지정된 업데이트를 지원 하지 않으며 delete 문, 하는 경우 이러한 드라이버를 시뮬레이션할 수 있습니다. 예를 들어 ODBC 커서 라이브러리 위치 지정된 업데이트를 시뮬레이션 하 고 delete 문입니다. 위치 지정된 update 및 delete 문 시뮬레이션 하기 위한 일반적인 전략 검색된 것을 위치 지정된 된 문을 변환 하는 것입니다. 대체 하 여 이렇게 합니다 **WHERE CURRENT OF** 절을 검색된 **여기서** 현재 행을 식별 하는 절.  
  
 예를 들어 CustID 열 Customers 테이블의 각 행을 고유 하 게 식별, 때문에 위치 지정 delete 문  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 변환 될 수 있습니다.  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 드라이버는 다음 중 하나를 사용할 수 있습니다 *행 식별자* 에 **여기서** 절:  
  
-   열 값을 가진 테이블의 모든 행에 고유 하 게 식별 하는 역할입니다. 예를 들어, 호출 **SQLSpecialColumns** SQL_BEST_ROWID를 사용 하 여 최적 열 또는이 용도로 사용 되는 열 집합을 반환 합니다.  
  
-   모든 행을 고유 하 게 식별 하기 위해 일부 데이터 원본의 경우 제공한 의사 (pseudo) 열입니다. 이러한 수도 검색할 호출한 **SQLSpecialColumns**합니다.  
  
-   사용 가능한 경우 고유 인덱스입니다.  
  
-   결과 집합의 모든 열  
  
 드라이버를 사용 해야 하는 열을 정확 하 게 합니다 **여기서** 절 생성 드라이버에 따라 달라 집니다. 일부 데이터 원본에서 행 식별자를 결정 비용이 많이 들 수 있습니다. 그러나가 더 빠르게 실행 하 고 시뮬레이션 된 문을 업데이트 하거나 적어도 하나 이상의 행을 삭제를 보장 합니다. 기본 DBMS의 기능에 따라 행 식별자를 사용 하 여 수를 설정 하는 데 비용이 많이 드는. 그러나가 더 빠르게 실행 하 고 시뮬레이션 된 문을 업데이트 하거나 하나의 행만 삭제 됩니다는 보장 합니다. 결과 집합의 모든 열을 사용 하는 옵션은 일반적으로 훨씬 쉽게 설정할 수 있습니다. 그러나 실행 하는 것이 느립니다 및 열 행을 고유 하 게 식별 하지 않는 행 실수로 업데이트 하거나 삭제 하면, 특히 select 목록 결과에 설정 된 경우에 없는 경우 기본 테이블에 있는 모든 열입니다.  
  
 지원 드라이버는 위의 전략에 따라, 응용 프로그램 전략 좋 SQL_ATTR_SIMULATE_CURSOR 문 특성을 사용 하는 드라이버를 선택할 수 있습니다. 응용 프로그램을 업데이트 하거나 행을 삭제 하면 의도 하지 않게 위험 홀수 보일 수 있습니다, 있지만 응용 프로그램 결과 집합의 열을 결과 집합의 각 행을 고유 하 게 식별 하 여이 위험을 제거할 수 있습니다. 이 작업을 수행 하지 않아도 활동 드라이버 저장 됩니다.  
  
 가로챌 드라이버 행 식별자를 사용 하도록 선택 하면 합니다 **SELECT FOR UPDATE** 문 결과 집합입니다. Select 목록의 열을 효과적으로 행을 나타내지 않으면, 드라이버 선택 목록의 끝에 필요한 열을 추가 합니다. 일부 데이터 원본에는 Oracle; ROWID 열과 같이 행을 고유 하 게 항상 하 게 식별 하는 단일 열 이러한 열 사용 가능한 경우이 드라이버를 사용 합니다. 드라이버를 호출 하는 고, 그렇지 **SQLSpecialColumns** 각 테이블에는 **FROM** 각 행을 고유 하 게 식별 하는 열 목록을 검색 하려면 절. 이 기법을 결과로 생성 되는 일반적인 제한은 커서 시뮬레이션에서 둘 이상의 테이블이 있으면 실패 하는 **FROM** 절.  
  
 드라이버가 행을 식별 하는 방법에 관계 없이 일반적으로 제거 합니다 **FOR UPDATE OF** off 절을 **SELECT FOR UPDATE** 데이터 원본에 전송 하기 전에 문을 합니다. 합니다 **업데이트의** 절을 사용 하 여 업데이트를 배치 하 고 delete 문을 사용 합니다. 지원 하지 않는 데이터 원본 위치 업데이트 및 delete 문은 일반적으로 지원 하지 않습니다.  
  
 드라이버 응용 프로그램에서 위치 지정된 update 또는 delete 문 실행을 제출 하는 경우 대체는 **WHERE CURRENT OF** 절을 **여기서** 행 식별자를 포함 하는 절. 이러한 열의 값이 사용 하 여 각 열에 대해 드라이버에서 유지 관리 캐시에서 검색 된 **여기서** 절. 드라이버 바뀐 후에 **여기서** 절 보냅니다 문 실행에 대 한 데이터 원본에 있습니다.  
  
 예를 들어, 응용 프로그램이 결과 집합을 만들려면 다음 문을 제출 한다고 가정 합니다.  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 응용 프로그램 요청 고유성을 보장 하려면 SQL_ATTR_SIMULATE_CURSOR이 설정 되 고 드라이버를 호출 하는 데이터 원본의 행을 고유 하 게 항상 하 게 식별 하는 의사 (pseudo) 열을 제공 하지 않으면 하는 경우 **SQLSpecialColumns** 에 CustID는 Customers 테이블에 키가 고 select 목록에 추가 및 제거는 customers 테이블을 검색 합니다 **FOR UPDATE OF** 절:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 응용 프로그램에 고유성을 보장 하는 요청 되지 않은 경우 드라이버만 제거 합니다 **FOR UPDATE OF** 절:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 여기서 Cust 이름인 커서의 결과 집합에 대해 응용 프로그램 결과 집합을 스크롤할 및 실행에 대 한 다음 현재 위치 업데이트 문을 전송 가정 합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 드라이버를 대체 하는 응용 프로그램에 고유성을 보장 하는 요청 되지 않은 경우는 **여기서** 절 하 고 해당 캐시에서 변수 CustID 매개 변수를 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 드라이버를 대체 하는 응용 프로그램에 고유성을 보장 하는 요청 되지 않은 경우는 **여기서** 절 및 해당 캐시에서 변수를이 절에서 이름, 주소 및 전화 매개 변수를 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
