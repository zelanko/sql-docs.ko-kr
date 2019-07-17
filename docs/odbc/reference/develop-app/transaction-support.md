---
title: 트랜잭션 지원 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0b5e33f94c5452a2062f7c18339f27c8da73fa9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086063"
---
# <a name="transaction-support"></a>트랜잭션 지원
트랜잭션에 대 한 지원 정도 드라이버 정의 됩니다. ODBC가 해당 데이터에 여러 업데이트를 관리할 필요가 없는 단일 사용자 또는 데스크톱 데이터베이스에서 구현 하도록 설계 되었습니다. 일부 데이터베이스 트랜잭션을 지 원하는 SQL, 데이터 조작 언어 (DML) 문의 경우에 수행 하는 또한 제한 또는 특별 한 트랜잭션 의미 체계 데이터 정의 언어 (DDL)의 사용에 대 한 트랜잭션이 활성 중일 때. 즉, 수 및 트랜잭션 중 테이블의 정의 변경 하지 않습니다 테이블에 여러 동시 업데이트에 대 한 트랜잭션 지원이 있을 수 있습니다.  
  
 응용 프로그램 트랜잭션이 지원 되는지 여부를 DDL 트랜잭션 및 호출 하 여 DDL 트랜잭션에서 등의 특수 한 효과에 포함 될 수 있는지 여부를 결정 **SQLGetInfo** SQL_TXN_CAPABLE 옵션을 사용 합니다. 자세한 내용은 참조는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.  
  
 드라이버는 트랜잭션을 지원 하지 않습니다. 응용 프로그램 데이터의 잠금을 해제 (이외의 ODBC API를 사용 하 여) 수 있습니다 하지만 응용 프로그램 잠금 및 잠금 해제 레코드 및 필요에 따라 테이블에서 트랜잭션 지원을 얻을 수 있습니다. 계정 전송 예제를 구현 하려면 응용 프로그램은 두 계정 모두에 대 한 레코드 잠금, 현재 값을 복사, 첫 번째 계좌에서 금액, 두 번째 계정 크레딧 및 레코드를 잠금 해제 모든 단계에 실패 한 경우 응용 프로그램 복사본을 사용 하 여 계정을 다시 설정 됩니다.  
  
 트랜잭션을 지 원하는 데이터 원본 특정 환경 내에서 한 번에 둘 이상의 트랜잭션을 지원할 수 있습니다. 응용 프로그램 호출 **SQLGetInfo** SQL_MULTIPLE_ACTIVE_TXN 옵션을 데이터 소스를 동일한 환경에서 둘 이상의 연결에서 동시 활성 트랜잭션을 지원 하는지 확인 합니다. 연결당 하나의 트랜잭션 이기 때문에이 동일한 데이터 소스에 여러 연결 되는 응용 프로그램 흥미로운만.
