---
title: SET REPROCESS 명령 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41877986d5d0e8afdfb30841860df360efd26da0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159376"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 명령
잠금 시도가 실패 한 파일이 나 레코드일 잠기도록 방법 또는 시간에 얼마나 많은 시간을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>인수  
 TO *nAttempts*[SECONDS]  
 횟수 또는 실패 한 초기 시도 후 레코드나 파일 잠금을 시도 시간 (초)을 지정 합니다. 기본값은 0입니다. 최대값은 32,000 합니다.  
  
 시간 (초) 지정 Visual FoxPro 파일을 잠그거나에 대 한 레코드를 시도 한다고 *nAttempts* 시간 (초)입니다. 인 경우에만 사용할 수 있습니다 *nAttempts* 0 보다 큽니다.  
  
 예를 들어 있으면 *nAttempts* 30, Visual FoxPro 레코드 잠금 또는 최대 30 배 파일 하려고 합니다. 또한 초 (30 다시 처리 설정 초)을 포함 하는 경우 Visual FoxPro 지속적으로 레코드 또는 파일을 최대 30 초 동안 잠금을 시도 합니다.  
  
 ON ERROR 루틴에 적용 되는 경우와 레코드 또는 파일을 잠글 명령에 의해 시도가 있으면 ON ERROR 루틴이 실행 됩니다. 그러나 잠금을 시도 하는 함수에는 ON ERROR 루틴 실행 되지 않습니다 하 고 함수가 False를 반환 합니다. (합니다. 6.).  
  
 ON ERROR 루틴에는 적용 되지 않습니다 하 고 명령을 레코드 또는 파일 잠금 하려고 잠금을 배치할 수 없습니다, 경우에 오류가 생성 됩니다. 함수에 잠금을 배치 하려고 하는 경우 경고가 표시 되지 않으면 및 함수가 False를 반환 합니다. (합니다. 6.).  
  
 하는 경우 *nAttempts* 0 (기본값) 명령 또는 레코드 또는 파일 잠금을 시도 하는 함수를 실행 하며, Visual FoxPro 레코드를 잠그지 또는 무기한 파일 하려고 합니다. 레코드 또는 파일을 사용할 수 있을 때까지 잠그기 위한 되 면 잠금을 배치 되 고 시스템 메시지 지워집니다. 함수 잠금을 배치를 시도 하는 경우 함수가 True를 반환 합니다 (합니다. 화) 합니다.  
  
 ON ERROR 루틴에 적용 되는 경우 명령을 레코드 또는 파일 잠금 하려고 합니다. ON ERROR 루틴 레코드 또는 파일 잠금을 설정 하려는 추가 시도가 보다 우선 합니다. ON ERROR 루틴은 즉시 실행 됩니다. Visual FoxPro 추가 레코드 또는 파일 잠금을 시도 하지 않습니다 및 시스템 메시지를 표시 하지 않습니다.  
  
 하는 경우 *nAttempts* 은 1이 고, Visual FoxPro 레코드를 잠그지 또는 무기한 파일 하려고 ON 오류 루틴 실행 되지 않습니다.  
  
 레코드 또는 잠금 하려고 하는 파일에서 다른 사용자가 잠금을 배치 된 경우 사용자 잠금이 해제 될 때까지 기다려야 합니다.  
  
 자동으로  
 Visual FoxPro 레코드를 잠그지 또는 무기한으로 파일을 시도 한다고 지정 합니다. (-2로 설정 다시 처리는 해당 하는 명령입니다.)  
  
## <a name="remarks"></a>Remarks  
 첫 번째 레코드 또는 파일 잠금을 시도 하지 못한 항상 합니다. 자주, 레코드 또는 파일을 네트워크의 다른 사용자에 의해 잠겨 있습니다. 설정 다시 처리 Visual FoxPro 초기 시도가 성공할 경우 레코드 또는 파일 잠금 추가 하려고 하면 여부를 결정 합니다. 하거나 추가 시도 하거나 시도 기간에 대 한 내용이 몇 번 지정할 수 있습니다. ON ERROR 루틴을 어떻게 실패 한 잠금을 시도 처리 되는 영향을 줍니다.
