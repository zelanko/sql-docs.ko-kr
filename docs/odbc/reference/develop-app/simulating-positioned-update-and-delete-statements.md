---
title: "Update 및 Delete 문을 배치 시뮬레이션 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 99d022dd56700a3e6441413eb43c06bc1c51cb70
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="simulating-positioned-update-and-delete-statements"></a>위치 지정된 Update 및 Delete 문을 시뮬레이션
데이터 원본 위치 지정된 업데이트를 지원 하지 않으며 delete 문의 하는 경우 이러한 드라이버 시뮬레이션할 수 있습니다. 예를 들어 ODBC 커서 라이브러리 시뮬레이션 위치 지정된 update 및 delete 문을 합니다. 위치 지정된 update 및 delete 문을 시뮬레이트하기 위한 일반적인 전략 검색 결과 프로토콜로 위치 지정 된 문을 변환 하는 것입니다. 대체 하 여 이렇게는 **WHERE CURRENT OF** 절은 검색 결과를 **여기서** 현재 행을 식별 하는 절.  
  
 예를 들어 CustID 열 Customers 테이블의 각 행을 고유 하 게 식별, 하기 때문에 위치 지정 delete 문  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 변환 될 수 있습니다.  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 드라이버는 다음 중 하나를 사용할 수 *행 식별자* 에 **여기서** 절:  
  
-   열 값을 가진 테이블의 모든 행에 고유 하 게 식별 하는 역할만 합니다. 예를 들어 호출 **SQLSpecialColumns** SQL_BEST_ROWID 최적 열 또는이 용도로 사용 되는 열 집합을 반환 합니다.  
  
-   의사 열-모든 행을 고유 하 게 식별 하기 위해 일부 데이터 원본에서 제공 합니다. 또한 장치일 수 검색 가능 호출 하 여 **SQLSpecialColumns**합니다.  
  
-   사용 가능한 경우 고유 인덱스입니다.  
  
-   결과 집합의 모든 열  
  
 에 드라이버를 사용 해야 하는 열을 정확 하 게는 **여기서** 생성 절 드라이버에 따라 달라 집니다. 일부 데이터에서 원본 행 식별자를 결정 하는 비용이 증가할 수 있습니다. 그러나 실행 하는 빠르고 시뮬레이션 된 문을 업데이트 하거나 행만 삭제를 보장 합니다. 기본 DBMS의 기능에 따라 행 식별자를 사용 하 여 수를 설정 하는 데 비용이 합니다. 그러나 실행 하는 빠르고 보장 시뮬레이션 된 문이 업데이트 되거나 하나의 행만 삭제 됩니다. 결과 집합의 모든 열을 사용 하 여 옵션은 일반적으로 훨씬 쉽게 설정할 수 있습니다. 그러나 실행 하는 것이 느립니다 및 열은 행을 고유 하 게 식별 하지 않습니다, 실수로 업데이트 또는 삭제할 행에 발생할 수 있습니다, 결과 대 한 선택 목록 설정에 없는 경우 기본 테이블에 있는 모든 열입니다.  
  
 지원 드라이버는 위의 전략에 따라, 응용 프로그램을 SQL_ATTR_SIMULATE_CURSOR 문 특성을 사용 하면 드라이버 브로드캐스트하며 전략을 선택할 수 있습니다. 실수로 업데이트 하거나 행을 삭제 되어도 응용 프로그램에 대 한 홀수 보이기는 하지만 응용 프로그램 결과 집합의 열 결과 집합의 각 행을 고유 하 게 식별 되도록 하 여 이러한 위험을 제거할 수 있습니다. 이 작업을 수행 하지 않고도 쉽게 드라이버 저장 됩니다.  
  
 차단 드라이버를 행 식별자를 사용 하기로 **업데이트에 대 한 선택** 문 결과 집합입니다. 선택 목록의 열 효과적으로 행을 나타내지 않으면, 드라이버 선택 목록의 끝에 필요한 열을 추가 합니다. 일부 데이터 원본 Oracle;에서 행 ID 열을 비롯 한 행을 항상 고유 하 게 식별 하는 단일 열에는 이러한 열에 표시 되 면 드라이버는이 사용 하 여 합니다. 그렇지 않은 경우 드라이버 호출 **SQLSpecialColumns** 각 테이블에는 **FROM** 각 행을 고유 하 게 식별 하는 열의 목록을 검색 하는 절. 이 기술은 한 결과인 공용 제한을 둘 이상의 테이블에 있는 경우 커서 시뮬레이션 실패 하는지는 **FROM** 절.  
  
 일반적으로 제거 드라이버 행 식별 하는 방법,에 관계 없이 **FOR UPDATE OF** off 절은 **업데이트에 대 한 선택** 데이터 원본에 보내기 전에 문을 합니다. **업데이트의** 와 업데이트를 배치 하 고 delete 문에 절을 사용 합니다. 지원 하지 않는 데이터 소스 업데이트를 배치 하 고 delete 문은 일반적으로 지원 하지 않습니다.  
  
 드라이버를 대체 하는 응용 프로그램에서 위치 지정된 update 또는 delete 문 실행에 전송할 때는 **WHERE CURRENT OF** 절과 함께 **여기서** 행 식별자를 포함 하는 절. 이러한 열의 값에 사용 하 여 각 열에 대해 드라이버에서 유지 관리 되는 캐시에서 검색 됩니다는 **여기서** 절. 드라이버 바뀐 후에 **여기서** 절, 보내는 문을 실행에 대 한 데이터 원본에 있습니다.  
  
 예를 들어 응용 프로그램이 결과 집합을 만들려면 다음 문을 제출 한다고 가정 합니다.  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 응용 프로그램 요청 열의 고유성을 보장 하려면 SQL_ATTR_SIMULATE_CURSOR이 설정 되 고 데이터 원본이 항상 고유 하 게 한 행을 식별 하는 의사 열을 제공 하지 않는 경우 드라이버를 호출 하는 경우 **SQLSpecialColumns** 에 CustID는 Customers 테이블에 키가 고 select 목록에 추가 및 제거는 customers 테이블을 검색 된 **FOR UPDATE OF** 절:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 응용 프로그램에서 고유성을 보장을 요청 하지 않은 경우 드라이버 제거만 **FOR UPDATE OF** 절:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 여기서 Cust은 이름 커서의 결과 집합에 대해 응용 프로그램에서는 결과 집합 스크롤한 다음 위치 지정된 update 문을 실행 하기 위해 전송에 있다고 가정 합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 응용 프로그램에서 고유성을 보장을 요청 하지 않은 경우 드라이버 대체는 **여기서** 절 CustID 매개 변수는 캐시에서 변수를 바인딩합니다.  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 응용 프로그램에서 고유성을 보장을 요청 하지 않은 경우 드라이버 대체는 **여기서** 절과이 절을 캐시에 변수 이름, 주소 및 전화 매개 변수 바인딩:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```

