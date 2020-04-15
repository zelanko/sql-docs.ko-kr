---
title: 거래 지원 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297981"
---
# <a name="transaction-support"></a>트랜잭션 지원
트랜잭션에 대한 지원 정도는 드라이버 정의입니다. ODBC는 데이터에 대한 여러 업데이트를 관리할 필요가 없는 단일 사용자 또는 데스크톱 데이터베이스에서 구현되도록 설계되었습니다. 또한 트랜잭션을 지원하는 일부 데이터베이스는 SQL의 DML(데이터 조작 언어) 문에 대해서만 그렇게 합니다. 트랜잭션이 활성화되어 있을 때 DDL(데이터 정의 언어) 사용에 대한 제한 또는 특별 트랜잭션 의미체계가 있습니다. 즉, 테이블에 대한 여러 동시 업데이트에 대한 트랜잭션 지원이 있을 수 있지만 트랜잭션 중에 테이블의 수와 정의를 변경하는 것은 아닙니다.  
  
 응용 프로그램은 트랜잭션이 지원되는지 여부, DDL을 트랜잭션에 포함할 수 있는지 여부 및 SQL_TXN_CAPABLE 옵션으로 **SQLGetInfo를** 호출하여 트랜잭션에 DDL을 포함하는 특수 효과를 결정합니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조하십시오.  
  
 드라이버가 트랜잭션을 지원하지 않지만 응용 프로그램에 ODBC 이외의 API를 사용하여 데이터를 잠그고 잠금을 해제하는 기능이 있는 경우 응용 프로그램은 필요에 따라 레코드와 테이블을 잠그고 잠금 해제하여 트랜잭션 지원을 얻을 수 있습니다. 계정 이전 예제를 구현하기 위해 응용 프로그램은 두 계정의 레코드를 잠그고, 현재 값을 복사하고, 첫 번째 계정을 인출하고, 두 번째 계정을 신용하고, 레코드의 잠금을 해제합니다. 단계가 실패하면 응용 프로그램은 복사본을 사용하여 계정을 재설정합니다.  
  
 트랜잭션을 지원하는 데이터 원본도 특정 환경 내에서 한 번에 두 개 이상의 트랜잭션을 지원하지 못할 수 있습니다. 응용 프로그램은 **sqlGetInfo를** SQL_MULTIPLE_ACTIVE_TXN 옵션으로 호출하여 데이터 원본이 동일한 환경에서 두 개 이상의 연결에서 동시에 활성 트랜잭션을 지원할 수 있는지 여부를 결정합니다. 연결당 트랜잭션이 하나 있기 때문에 동일한 데이터 원본에 여러 연결이 있는 응용 프로그램에만 흥미롭습니다.
