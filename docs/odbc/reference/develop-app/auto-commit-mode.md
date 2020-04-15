---
title: 자동 커밋 모드 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285113"
---
# <a name="auto-commit-mode"></a>자동 커밋 모드
*자동 커밋 모드에서* 모든 데이터베이스 작업은 수행할 때 커밋되는 트랜잭션입니다. 이 모드는 단일 SQL 문으로 구성된 많은 실제 트랜잭션에 적합합니다. 이러한 트랜잭션의 완료를 구분하거나 지정할 필요는 없습니다. 트랜잭션 지원이 없는 데이터베이스에서는 자동 커밋 모드가 유일한 지원 모드입니다. 이러한 데이터베이스에서 문은 실행될 때 커밋되며 롤백할 방법이 없습니다. 따라서 항상 자동 커밋 모드에 있습니다.  
  
 기본 DBMS가 자동 커밋 모드 트랜잭션을 지원하지 않는 경우 드라이버는 실행될 때 각 SQL 문을 수동으로 커밋하여 에뮬레이트할 수 있습니다.  
  
 SQL 문 일괄 처리가 자동 커밋 모드에서 실행되는 경우 일괄 처리의 문이 커밋될 때 데이터 원본에 따라 다릅니다. 전체 일괄 처리가 실행된 후 실행될 때 또는 전체적으로 커밋할 수 있습니다. 일부 데이터 원본은 이러한 동작을 모두 지원할 수 있으며 하나 또는 다른 동작을 선택하는 방법을 제공할 수 있습니다. 특히 일괄 처리 중간에 오류가 발생하는 경우 이미 실행된 문이 커밋되거나 롤백되는지 여부에 따라 데이터 원본에 따라 다릅니다. 따라서 일괄 처리를 사용하고 전체적으로 커밋하거나 롤백해야 하는 상호 운용 가능한 응용 프로그램은 수동 커밋 모드에서만 일괄 처리를 실행해야 합니다.
