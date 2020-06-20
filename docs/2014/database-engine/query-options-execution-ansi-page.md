---
title: 쿼리 옵션 실행 (ANSI 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: rothja
ms.author: jroth
ms.openlocfilehash: 088068bd4ddd70879efa606b22b186eb4839eaf6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929654"
---
# <a name="query-options-execution-ansi-page"></a>쿼리 옵션 실행(ANSI 페이지)
  이 페이지를 사용 하 여에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ISO (ANSI) 표준에 지정 된 설정의 일부 또는 전부를 사용 하 여 쿼리를 실행 하도록 지정할 수 있습니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 **SET ANSI_DEFAULTS**  
 기본 ISO 설정을 모두 선택합니다. 일부 ISO 설정만 구성되어 있으므로 이 상자는 기본적으로 비활성화되어 있습니다.  
  
 **SET QUOTED_IDENTIFIER**  
 개체 식별자 앞뒤에 따옴표를 표시합니다. 이 옵션은 기본적으로 선택됩니다.  
  
 **SET ANSI_NULL_DFLT_ON**  
 CREATE TABLE 또는 ALTER TABLE 문(기본 상태)을 실행하는 동안 NOT NULL로 명시적으로 정의되지 않은 모든 사용자 정의 데이터 형식 또는 열에서 Null 값을 허용합니다. 이 옵션은 기본적으로 선택됩니다.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 이 옵션은 기본적으로 선택되어 있지 않습니다.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 트랜잭션이 커밋되면 ISO에 따라 열려 있는 모든 커서를 자동으로 닫습니다. 이 옵션의 선택을 취소(OFF로 설정)하면 커서는 트랜잭션이 바뀌어도 계속 열려 있으며 연결이 닫히거나 커서를 명시적으로 닫아야만 닫힙니다. 이 옵션은 기본적으로 선택되어 있지 않습니다.  
  
 **SET ANSI_PADDING**  
 열이 정의 된 열 크기 보다 짧은 값을 저장 하는 방법과 **char**, **varchar**, **binary**및 **varbinary** 데이터에 후행 공백이 있는 값을 저장 하는 방법을 제어 합니다. 이 설정은 새 열의 정의에만 영향을 줍니다. 열이 생성된 다음에는 열을 만들 때의 설정에 따라 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 값을 저장합니다. 나중에 이 설정을 변경해도 기존의 열은 영향을 받지 않습니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **SET ANSI_WARNINGS**  
 여러 오류 상황에 대한 ISO 표준 동작을 지정합니다.  
  
-   이 확인란을 선택하면 SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP 또는 COUNT와 같은 집계 함수에 Null 값이 나타나는 경우에 경고 메시지가 생성됩니다. **OFF**인 경우 경고가 발생 하지 않습니다.  
  
-   이 확인란의 선택을 취소한 경우 0으로 나누기 및 산술 오버플로 오류가 발생하면 문이 롤백되고 오류 메시지가 생성됩니다. OFF로 설정한 경우 0으로 나누기 및 산술 오버플로 오류가 발생하면 Null 값이 반환됩니다. 새 값의 길이가 열의 최대 크기를 초과하는 character, Unicode 또는 binary 열에 INSERT나 UPDATE 작업을 하려고 하면 0으로 나누기 또는 산술 오버플로 오류로 인해 Null 값이 반환될 수 있습니다. **SET ANSI_WARNINGS** ON 이면 ISO 표준에 지정 된 대로 삽입 또는 업데이트 작업이 취소 됩니다. 문자 열에 대해서는 후행 공백이, 이진 열에 대해서는 후행 Null 값이 무시됩니다. 이 옵션이 OFF이면 열의 크기에 맞게 데이터가 잘리고 문이 성공적으로 실행됩니다.  
  
 이 옵션은 기본적으로 선택됩니다.  
  
 **SET ANSI_NULLS**  
 같음(`=`)과 같지 않음(`<>`) 비교 연산자를 Null 값과 함께 사용할 경우의 ISO 호환 동작을 지정합니다. **SET ANSI_NULLS** 를 선택하면 데이터와 Null 값을 비교한 결과가 ISO 호환 동작에 따라 UNKNOWN이 됩니다. **SET ANSI_NULLS** 를 선택하지 않으면 데이터 값이 NULL일 때 Null 값에 대한 모든 데이터 비교의 결과가 TRUE가 됩니다. 이 옵션은 기본적으로 선택됩니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
