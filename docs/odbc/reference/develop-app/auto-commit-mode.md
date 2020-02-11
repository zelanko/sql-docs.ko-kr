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
ms.openlocfilehash: a8a02d58309f123e6cc8b29d41188ba5bebb26f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67909897"
---
# <a name="auto-commit-mode"></a>자동 커밋 모드
*자동 커밋 모드에서* 모든 데이터베이스 작업은 수행할 때 커밋된 트랜잭션입니다. 이 모드는 단일 SQL 문으로 구성 된 많은 실제 트랜잭션에 적합 합니다. 이러한 트랜잭션의 완료를 구분 하거나 지정 하는 것은 필요 하지 않습니다. 트랜잭션 지원이 없는 데이터베이스에서 자동 커밋 모드는 유일 하 게 지원 되는 모드입니다. 이러한 데이터베이스에서 문은 실행 될 때 커밋되고 롤백할 방법이 없습니다. 따라서 항상 자동 커밋 모드가 됩니다.  
  
 기본 DBMS에서 자동 커밋 모드 트랜잭션을 지원 하지 않는 경우 드라이버는 실행 될 때마다 각 SQL 문을 수동으로 커밋하여이를 에뮬레이트할 수 있습니다.  
  
 자동 커밋 모드에서 SQL 문 일괄 처리를 실행 하는 경우 일괄 처리의 문이 커밋될 때 데이터 원본에 해당 합니다. 이러한 작업은 전체 일괄 처리가 실행 된 후 실행 되거나 전체적으로 커밋될 수 있습니다. 일부 데이터 원본은 이러한 동작을 둘 다 지원할 수 있으며 하나 또는 다른 데이터를 선택 하는 방법을 제공할 수 있습니다. 특히 일괄 처리 중간에 오류가 발생 하는 경우이는 이미 실행 된 문이 커밋 또는 롤백 되었는지 여부에 관계 없이 데이터 원본에 해당 합니다. 따라서 일괄 처리를 사용 하 고 전체적으로 커밋되거나 롤백해야 하는 상호 운용 가능한 응용 프로그램은 수동 커밋 모드 에서만 일괄 처리를 실행 해야 합니다.
