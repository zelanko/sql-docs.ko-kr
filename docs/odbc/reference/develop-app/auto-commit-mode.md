---
title: "자동 커밋 모드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb9b6d354657578f7188481a2e7ff7566f725c80
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="auto-commit-mode"></a>자동 커밋 모드
*자동 커밋 모드에서* 모든 데이터베이스 작업은 수행 될 때 커밋됩니다. 이 모드는 단일 SQL 문으로 구성 된 여러 실제 트랜잭션이에 적합 합니다. 구분 하거나 이러한 트랜잭션이 완료를 지정할 필요는 없습니다. 트랜잭션 지원 없이 데이터베이스, 자동 커밋 모드는 지원 되는 유일한 모드는 있습니다. 이러한 데이터베이스에서는 문이 커밋됩니다 때 실행 되 고 롤백; 방식은 없습니다. 따라서 항상에 않습니다 자동 커밋 모드.  
  
 기본 DBMS 자동 커밋 모드 트랜잭션을 지원 하지 않는 경우 드라이버를 실행할 때 각 SQL 문을 수동으로 커밋하여이 에뮬레이트할 수 있습니다.  
  
 SQL 문의 일괄 처리는 자동 커밋 모드에서 실행 되는 일괄 처리의 문이 커밋됩니다 때 데이터 원본에 따른 특정 실행 됩니다. 커밋하려면 실행 또는 전체적으로 전체 일괄 처리가 실행 된 후입니다. 일부 데이터 원본 모두 이러한 동작을 지원할 수 있습니다 및 하나 또는 다른 항목을 선택 하는 방법을 제공할 수 있습니다. 특히, 일괄 처리 중에 오류가 발생할 경우 데이터 원본에 따른 특정 이미 실행 된 문이 커밋 또는 롤백 여부입니다. 따라서 수 트랜잭션이 커밋 또는 롤백됨을 전체적으로 록 및 일괄 처리를 사용 하는 상호 운용 가능한 응용 프로그램 수동 커밋 모드에만 일괄 처리를 실행 해야 합니다.
