---
title: '방법: 함수, 트리거 및 저장 프로시저에 대한 SQL Server 단위 테스트 만들기 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bda57c10-a1ab-4a1a-8a71-42085a3cb793
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: adb8d905c6ed2a5b3c6c20ec5feb595981920da8
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094688"
---
# <a name="how-to-create-sql-server-unit-tests-for-functions-triggers-and-stored-procedures"></a>방법: 함수, 트리거 및 저장 프로시저에 대한 SQL Server 단위 테스트 만들기
데이터베이스 개체에 대한 변경 내용을 평가하는 단위 테스트를 작성할 수 있습니다. 그러나 SQL Server Data Tools에는 SQL Server 개체 탐색기의 데이터베이스 프로젝트 노드에서 데이터베이스 함수, 트리거 및 저장 프로시저에 대한 테스트를 만들기 위한 추가 지원 기능이 포함되어 있습니다. Transact\-SQL 코드 스텁이 자동으로 생성되며 이를 사용자 지정할 수 있습니다.  
  
### <a name="to-create-a-sql-server-unit-test-from-a-function-trigger-or-stored-procedure"></a>함수, 트리거 또는 저장 프로시저에서 SQL Server 단위 테스트를 만들려면  
  
1.  저장 프로시저에 대한 SQL Server 단위 테스트를 추가하는 예는 [연습: SQL Server 단위 테스트 만들기 및 실행](../ssdt/walkthrough-creating-and-running-a-sql-server-unit-test.md)의 “저장 프로시저에 대한 SQL Server 단위 테스트를 만들려면” 섹션을 참조하세요.  
  
    결과 불충분 테스트 조건은 모든 테스트에 추가되는 기본 조건입니다. 이 테스트 조건은 테스트 확인이 구현되지 않았음을 나타내기 위해 포함됩니다. 이 테스트 조건은 다른 테스트 조건을 추가한 후 테스트에서 삭제합니다. 자세한 내용은 [방법: SQL Server 단위 테스트에 테스트 조건 추가](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 만들기 및 정의](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[방법: 빈 SQL Server 단위 테스트 만들기](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
  
