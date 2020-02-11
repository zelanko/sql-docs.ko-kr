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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086063"
---
# <a name="transaction-support"></a>트랜잭션 지원
트랜잭션에 대 한 지원 수준은 드라이버에 정의 되어 있습니다. ODBC는 데이터에 대 한 여러 업데이트를 관리할 필요가 없는 단일 사용자 또는 데스크톱 데이터베이스에서 구현 되도록 설계 되었습니다. 또한 트랜잭션을 지 원하는 일부 데이터베이스는 SQL의 DML (데이터 조작 언어) 문에 대해서만 수행 합니다. 트랜잭션이 활성 상태일 때 DDL (데이터 정의 언어) 사용과 관련 된 제한 사항 또는 특별 한 트랜잭션 의미 체계가 있습니다. 즉, 테이블에 대 한 여러 동시 업데이트에 대 한 트랜잭션 지원이 있을 수 있으며 트랜잭션 중에 테이블의 수와 정의를 변경할 수 없습니다.  
  
 응용 프로그램은 트랜잭션이 지원 되는지 여부, DDL을 트랜잭션에 포함할 수 있는지 여부, SQL_TXN_CAPABLE 옵션으로 **SQLGetInfo** 를 호출 하 여 트랜잭션에 ddl을 포함 하는 특별 한 효과를 결정 합니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명을 참조 하세요.  
  
 드라이버가 트랜잭션을 지원 하지 않지만 응용 프로그램이 데이터를 잠그고 잠금 해제할 수 있는 기능이 있는 경우, 응용 프로그램은 필요에 따라 레코드와 테이블을 잠그고 잠금 해제 하 여 트랜잭션 지원을 얻을 수 있습니다. 계정 전송 예제를 구현 하기 위해 응용 프로그램은 두 계정 모두에 대 한 레코드를 잠그고, 현재 값을 복사 하 고, 첫 번째 계정을 지불 하 고, 두 번째 계정을 크레딧 하 고, 레코드의 잠금을 해제 합니다. 실패 한 단계가 있으면 응용 프로그램은 복사본을 사용 하 여 계정을 다시 설정 합니다.  
  
 트랜잭션을 지 원하는 데이터 원본에도 특정 환경 내에서 한 번에 둘 이상의 트랜잭션을 지원 하지 못할 수 있습니다. 응용 프로그램은 SQL_MULTIPLE_ACTIVE_TXN 옵션으로 **SQLGetInfo** 를 호출 하 여 데이터 소스가 동일한 환경에서 두 개 이상의 연결에서 동시 활성 트랜잭션을 지원할 수 있는지 여부를 확인 합니다. 연결당 하나의 트랜잭션이 있기 때문에 동일한 데이터 원본에 대 한 여러 연결이 있는 응용 프로그램에만 관심이 있습니다.
