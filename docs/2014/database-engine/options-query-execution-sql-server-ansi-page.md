---
title: 옵션 (쿼리 실행-SQL Server-ANSI 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a3d8f15f159ea41590c67677c2d020f0a5dbc79a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774971"
---
# <a name="options-query-execution-sql-server-ansi-page"></a>옵션 (쿼리 실행-SQL Server-ANSI 페이지)
  이러한 ANSI(ISO) 표준 SET 옵션은 사용자 쿼리 실행 기간, 실행 중인 트리거, 저장 프로시저에 대해 쿼리 처리 환경을 정의합니다. 그러나 이러한 SET 옵션에 ISO 표준을 준수하는 데 필요한 모든 옵션이 포함되지는 않습니다. 이 페이지를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 ISO 표준에 지정되어 있는 설정의 일부 또는 전부를 사용하여 쿼리를 실행하도록 지정할 수 있습니다. 이러한 옵션의 변경 내용은 새로운 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리에만 적용됩니다. 현재 쿼리에 대한 옵션을 변경하려면 **쿼리** 메뉴에서 **쿼리 옵션**을 클릭하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 창에서 마우스 오른쪽 단추를 클릭한 다음 **쿼리 옵션**을 선택합니다. **쿼리 옵션** 대화 상자의 **실행**아래에서 **ANSI**를 클릭합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **SET ANSI_DEFAULTS**  
 기본 ISO 설정을 모두 선택하려면 이 확인란을 선택합니다. 기본적으로 모든 ISO 옵션이 선택되지는 않습니다.  
  
 **SET QUOTED_IDENTIFIER**  
 이 확인란을 선택하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 따옴표로 구분된 식별자 및 리터럴 문자열과 관련해서 ISO 규칙을 따릅니다. 따옴표로 구분된 식별자는 Transact-SQL의 예약된 키워드이거나 Transact-SQL 식별자 구문 규칙에서 허용하지 않는 문자를 포함할 수 있습니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **SET ANSI_NULL_DFLT_ON**  
 이 값을 설정하면 CREATE TABLE 또는 ALTER TABLE 문에서 명시적으로 NOT NULL로 정의되지 않은 모든 사용자 정의 데이터 형식 또는 열에 기본적으로 Null 값이 허용됩니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 SET IMPLICIT_TRANSACTIONS 확인란을 선택하면 연결이 암시적 트랜잭션 모드로 설정됩니다. 이 확인란의 선택을 취소하면 연결은 다시 자동 커밋 트랜잭션 모드로 돌아갑니다. 선택 시 암시적 트랜잭션을 시작하는 문을 보려면 [SET IMPLICIT_TRANSACTIONS&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-implicit-transactions-transact-sql)를 참조하세요. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 이 확인란을 선택하면 트랜잭션이 커밋될 때 열려 있던 모든 커서가 ISO에 따라 자동으로 닫힙니다. 이 값을 OFF로 설정하면 커서는 트랜잭션이 바뀌어도 계속 열려 있으며 연결이 닫히거나 커서를 명시적으로 닫아야만 닫힙니다. 이 확인란은 기본적으로 선택 취소되어 있습니다.  
  
 **SET ANSI_PADDING**  
 열이 정의된 열 크기보다 짧은 값 이름을 저장하는 방법과 **char**, **varchar**, **binary**및 **varbinary** 데이터에 후행 공백이 있는 값을 저장하는 방법을 제어합니다. 이 설정은 새 열의 정의에만 영향을 줍니다. 열이 생성된 다음에는 열을 만들 때의 설정에 따라 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 값을 저장합니다. 나중에 이 설정을 변경해도 기존의 열은 영향을 받지 않습니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **SET ANSI_WARNINGS**  
 여러 오류 상황에 대한 ISO 표준 동작을 지정합니다.  
  
-   이 확인란을 선택하면 SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP 또는 COUNT와 같은 집계 함수에 Null 값이 나타나는 경우에 경고 메시지가 생성됩니다. OFF로 설정한 경우에는 경고가 발생하지 않습니다.  
  
-   이 확인란의 선택을 취소한 경우 0으로 나누기 및 산술 오버플로 오류가 발생하면 문이 롤백되고 오류 메시지가 생성됩니다. OFF로 설정한 경우 0으로 나누기 및 산술 오버플로 오류가 발생하면 Null 값이 반환됩니다. 새 값의 길이가 열의 최대 크기를 초과하는 **character**, **Unicode** 또는 **binary** 열에 INSERT나 UPDATE 작업을 하려고 하면 0으로 나누기 또는 산술 오버플로 오류로 인해 Null 값이 반환될 수 있습니다. SET ANSI_WARNINGS 옵션이 ON이면 ISO 표준에 지정된 대로 INSERT 또는 UPDATE 작업이 취소됩니다. 문자 열에 대해서는 후행 공백이, 이진 열에 대해서는 후행 NULL 값이 무시됩니다. 이 옵션이 OFF이면 열의 크기에 맞게 데이터가 잘리고 문이 성공적으로 실행됩니다.  
  
 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **SET ANSI_NULLS**  
 -   같음(=)과 같지 않음(<>) 비교 연산자를 Null 값과 함께 사용할 경우의 ISO 호환 동작을 지정합니다. SET ANSI_NULLS를 선택하면 데이터와 Null 값을 비교한 결과가 ISO 호환 동작에 따라 UNKNOWN이 됩니다. SET ANSI_NULLS를 선택하지 않으면 데이터와 Null 값을 비교한 결과가 모두 TRUE가 됩니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
