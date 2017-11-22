---
title: "SET 빈도로 명령을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8e907d01b79c314603ba87c8195e56c8710bd10
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="set-reprocess-command"></a>SET 빈도로 명령
실패 한 잠금 시도 후 파일이 나 레코드를 잠그는 수 시간 또는 방법에 대 한 long을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>인수  
 *nAttempts*[SECONDS]  
 횟수 또는 초기 실패 한 시도 후 레코드 또는 파일을 잠그려고 할 시간 (초)을 지정 합니다. 기본값은 0; 최대값은 32, 000입니다.  
  
 Visual FoxPro에 대 한 기록 하거나 파일을 잠금으로써을 하려고 (초) 지정 *nAttempts* 초입니다. 인 경우에만 사용할 수 있는 *nAttempts* 가 0 보다 큽니다.  
  
 예를 들어 경우 *nAttempts* 30, Visual FoxPro 레코드 잠금 또는 최대 30 배까지 파일을 시도 합니다. 또한 초 (30 다시 처리 설정 초)를 포함 하는 경우를 위해 잠글 레코드 또는 파일을 최대 30 초 Visual FoxPro 지속적으로 시도 합니다.  
  
 ON 오류 루틴 적용 되 고 레코드 또는 파일을 잠그려면 명령에 의해 시도가 ON 오류 루틴 실행 됩니다. 그러나 함수 잠금을 만들려고 할 경우, ON 오류 루틴 실행 하지 않으면 하 고 함수가 False를 반환 합니다. (합니다. 6.).  
  
 ON 오류 루틴에는 적용 되지 않습니다, 레코드 또는 파일을 잠그는 명령을 시도 잠금을 배치할 수 없습니다 오류가 생성 됩니다. 함수를 잠금을 배치 하려고 하는 경우 경고가 표시 되지 않으면 및 함수가 False를 반환 합니다. (합니다. 6.).  
  
 경우 *nAttempts* 0 (기본값) 명령 또는 레코드 또는 파일 잠금 하려고 하는 함수를 실행 하며, Visual FoxPro 레코드 잠금 또는 파일을 무기한 하려고 합니다. 레코드 또는 파일을 기다리는 동안 잠금에 사용할 수 있는 경우 잠금을 배치 되 고 시스템 메시지의 선택을 취소 합니다. 함수가 함수가 잠금을 배치 하려고 하는 경우 True를 반환 합니다 (합니다. 화) 합니다.  
  
 ON 오류 루틴 적용 되는 명령 레코드 또는 파일 잠금 하려고 하는 경우 ON 오류 루틴 레코드 또는 파일 잠금 하려는 추가 시도가 보다 우선 합니다. ON 오류 루틴 즉시 실행 됩니다. Visual FoxPro 추가 레코드 또는 파일 잠금을 시도 하지 않습니다 및 시스템 메시지를 표시 하지 않습니다.  
  
 경우 *nAttempts* 은 1이 고, Visual FoxPro 레코드 잠금 또는 파일을 무기한 하려고 ON 오류 루틴 실행 되지 않습니다.  
  
 레코드 또는 잠글 하려는 파일에서 다른 사용자가 잠금의 배치 하는 경우 사용자의 잠금을 해제 될 때까지 기다려야 합니다.  
  
 자동으로  
 Visual FoxPro 레코드 잠금 또는 무기한 파일을 시도 한다고 지정 합니다. (-2로 집합 빈도로 이와 동등한 명령을.)  
  
## <a name="remarks"></a>주의  
 레코드 또는 파일 잠금를 첫 번째 시도가 성공 항상 않습니다. 자주, 레코드 또는 파일을 네트워크에서 다른 사용자에 의해 잠겨 있습니다. 설정 다시 처리 Visual FoxPro 하면 추가 시도가 초기 시도가 성공한 경우 레코드 또는 파일을 잠글 수 있는지 여부를 결정 합니다. 하거나 추가 시도 하거나 기간 시도 대 한 내용이 몇 번 지정할 수 있습니다. ON 오류 루틴 어떻게 실패 한 잠금을 시도 처리 하는 영향을 줍니다.
