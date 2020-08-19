---
description: SET REPROCESS 명령
title: 다시 처리 명령 설정 | Microsoft Docs
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
ms.openlocfilehash: 8daeebd38f295d437dc02c1c34126c30f6426b68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421827"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 명령
잠금 시도가 실패 한 후 파일 또는 레코드를 잠글 시간 또는 시간을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>인수  
 *N 번 시도*[초]  
 초기 시도가 실패 한 후에 레코드나 파일의 잠금을 시도 하는 시간 또는 초 수를 지정 합니다. 기본값은 0입니다. 최대값은 32000입니다.  
  
 초는 Visual FoxPro에서 *nattempts* 시간 (초) 동안 파일 또는 레코드 잠금을 시도 하도록 지정 합니다. *Nattempts* 가 0 보다 큰 경우에만 사용할 수 있습니다.  
  
 예를 들어 *Nattempts* 가 30 인 경우 Visual FoxPro는 레코드나 파일을 최대 30 회 잠그려고 시도 합니다. 초도 포함 하는 경우 (다시 처리를 30 초로 설정) Visual FoxPro는 최대 30 초 동안 레코드나 파일의 잠금을 계속 시도 합니다.  
  
 ON ERROR 루틴이 적용 되 고 레코드 또는 파일을 잠그기 위한 명령의 시도에 실패 한 경우 ON ERROR 루틴이 실행 됩니다. 그러나 함수에서 잠금을 시도 하는 경우 ON ERROR 루틴이 실행 되지 않고 함수에서 False를 반환 합니다. F.).  
  
 ON ERROR 루틴이 적용 되지 않은 경우 명령이 레코드나 파일을 잠그려고 시도 하 고 잠금을 배치할 수 없으므로 오류가 발생 합니다. 함수에서 잠금을 시도 하면 경고가 표시 되지 않고 함수에서 False (. F.).  
  
 *Nattempts* 가 0 (기본값)이 고 레코드나 파일의 잠금을 시도 하는 명령이 나 함수를 실행 하는 경우 Visual FoxPro는 레코드나 파일을 무기한 잠금으로 시도 합니다. 대기 하는 동안 레코드 또는 파일을 잠금에 사용할 수 있게 되 면 잠금이 적용 되 고 시스템 메시지가 지워집니다. 함수에서 잠금을 시도 하려고 하면이 함수는 True를 반환 합니다. T.).  
  
 ON ERROR 루틴이 적용 되 고 명령이 레코드나 파일의 잠금을 시도 하는 경우 레코드 또는 파일을 잠그기 위한 추가 시도 보다 오류 발생 시 루틴이 우선적으로 적용 됩니다. ON ERROR 루틴이 즉시 실행 됩니다. Visual FoxPro는 추가 레코드나 파일 잠금을 시도 하지 않으며 시스템 메시지를 표시 하지 않습니다.  
  
 *Nattempts* 이 1 이면 Visual FoxPro에서 레코드 또는 파일을 무기한 잠금으로 시도 하 고 오류 발생 시 루틴이 실행 되지 않습니다.  
  
 잠금을 시도 하는 레코드나 파일에 다른 사용자가 잠금을 설정한 경우 사용자가 잠금을 해제할 때까지 기다려야 합니다.  
  
 자동으로  
 Visual FoxPro에서 레코드 또는 파일을 무기한 잠금으로 시도 하도록 지정 합니다. (다시 처리를-2로 설정 하는 것은 동일한 명령입니다.)  
  
## <a name="remarks"></a>설명  
 첫 번째 레코드나 파일의 잠금 시도는 항상 성공 하지는 않습니다. 종종 레코드나 파일이 네트워크의 다른 사용자에 의해 잠겨 있습니다. SET 다시 처리는 초기 시도가 실패할 때 Visual FoxPro에서 레코드 또는 파일 잠금을 추가로 시도할지를 결정 합니다. 추가 시도 횟수 또는 시도 시간을 지정할 수 있습니다. 오류 발생 시 루틴은 실패 한 잠금 시도를 처리 하는 방법에 영향을 줍니다.
