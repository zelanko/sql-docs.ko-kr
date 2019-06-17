---
title: 자동 커밋 모드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 491fb8db9e37cfb3bfa07881958fe7828e6bb911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048429"
---
# <a name="auto-commit-mode"></a>자동 커밋 모드
*자동 커밋 모드로* 모든 데이터베이스 작업이 수행 하는 경우 커밋된 트랜잭션입니다. 이 모드는 단일 SQL 문으로 구성 된 여러 실제 트랜잭션에 적합 합니다. 구분 하거나 이러한 트랜잭션의 완료를 지정할 필요는 없습니다. 트랜잭션 지원 하지 않는 데이터베이스에서 자동 커밋 모드로 지원 되는 모드가입니다. 이러한 데이터베이스에서는 문이 커밋되는 경우 실행 되 고 롤백; 방법이 있습니다. 되므로 항상 자동 커밋 모드에 있습니다.  
  
 기본 DBMS 트랜잭션을 자동 커밋하 모드를 지원 하지 않는 경우 드라이버를 실행할 때 각 SQL 문을 수동으로 커밋하여이 에뮬레이트할 수 있습니다.  
  
 자동 커밋 모드에서 SQL 문의 일괄 처리를 실행 하면 때 데이터 소스 특정 일괄 처리의 문이 커밋됩니다. 커밋할 수 있습니다 실행 될 때 또는 전체적으로 전체 일괄 처리가 실행 된 후. 일부 데이터 원본 모두 이러한 동작을 지원할 수 있습니다 및 하나 또는 다른 선택 하는 방법을 제공할 수 있습니다. 특히에 일괄 처리 중 오류가 발생 한 경우 데이터 소스 관련 이미 실행 문이 커밋 또는 롤백 하는지 여부를 있습니다. 따라서 일괄 처리를 사용 하 고 커밋 또는 롤백 전체적으로 해야 하는 상호 운용 가능한 응용 프로그램 수동 커밋 모드에만 일괄 처리를 실행 해야 합니다.
