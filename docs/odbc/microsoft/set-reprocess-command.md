---
title: 다시 처리 명령 설정 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a7eb5fd19ca538c4f25077926567011ae133e54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300833"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 명령
잠금 시도가 실패한 후 파일 또는 레코드를 잠글 수 있는 횟수 또는 시간을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>인수  
 to *n시도*[초]  
 초기 실패 시도 후 레코드 또는 파일을 잠글 수 있는 횟수 또는 초수를 지정합니다. 기본값은 0입니다. 최대값은 32,000입니다.  
  
 초는 Visual FoxPro가 *n시도* 초 동안 파일 또는 레코드를 잠그려고 시도하도록 지정합니다. *n시도가* 0보다 큰 경우에만 사용할 수 있습니다.  
  
 예를 들어 *n시도가* 30인 경우 Visual FoxPro는 레코드 또는 파일을 최대 30회 까지 잠그려고 시도합니다. 초(재처리 30초로 설정)도 포함하는 경우 Visual FoxPro는 레코드 또는 파일을 최대 30초 동안 계속 잠급니다.  
  
 ON ERROR 루틴이 적용되고 레코드 또는 파일을 잠그려는 명령의 시도가 실패하면 ON ERROR 루틴이 실행됩니다. 그러나 함수가 잠금을 시도하면 ON ERROR 루틴이 실행되지 않고 함수가 False(False)를 반환합니다. F.)를 참조하십시오.  
  
 ON ERROR 루틴이 적용되지 않으면 명령이 레코드 또는 파일을 잠그려고 시도하고 잠금을 배치할 수 없는 경우 오류가 생성됩니다. 함수가 잠금을 배치하려고 하면 경고가 표시되지 않고 함수가 False(False)를 반환합니다. F.)를 참조하십시오.  
  
 *nTries가* 0(기본값)이고 레코드 또는 파일을 잠그려고 시도하는 명령이나 함수를 발급하는 경우 Visual FoxPro는 레코드 또는 파일을 무기한 잠그려고 시도합니다. 기다리는 동안 레코드 또는 파일을 잠글 수 있게 되면 잠금이 배치되고 시스템 메시지가 지워집니다. 함수가 잠금을 배치하려고 하면 함수가 True(True)를 반환합니다. T.)를 참조하십시오.  
  
 ON ERROR 루틴이 적용되고 명령이 레코드 또는 파일을 잠그려고 하는 경우 ON ERROR 루틴이 레코드 또는 파일을 잠그려는 추가 시도보다 우선합니다. ON 오류 루틴이 즉시 실행됩니다. Visual FoxPro는 추가 레코드 또는 파일 잠금을 시도하지 않으며 시스템 메시지를 표시하지 않습니다.  
  
 *n시도가* 1이면 Visual FoxPro는 레코드 또는 파일을 무기한 잠그려고 시도하며 ON ERROR 루틴이 실행되지 않습니다.  
  
 다른 사용자가 잠그려는 레코드 나 파일에 잠금을 배치한 경우 사용자가 잠금을 해제할 때까지 기다려야 합니다.  
  
 자동으로  
 Visual FoxPro가 레코드 또는 파일을 무기한 잠그려고 시도하도록 지정합니다. (다시 처리 -2로 설정하는 것은 동일한 명령입니다.)  
  
## <a name="remarks"></a>설명  
 레코드 또는 파일을 잠그는 첫 번째 시도가 항상 성공한 것은 아닙니다. 네트워크의 다른 사용자가 레코드 또는 파일을 잠그는 경우가 자주 있습니다. SET REPROCESS는 Visual FoxPro가 초기 시도가 실패할 때 레코드 또는 파일을 잠그려고 추가 시도를 하는지 여부를 결정합니다. 추가 시도가 이루어진 횟수 또는 시도가 이루어진 시간을 지정할 수 있습니다. ON ERROR 루틴은 실패한 잠금 시도를 처리하는 방법에 영향을 줍니다.
