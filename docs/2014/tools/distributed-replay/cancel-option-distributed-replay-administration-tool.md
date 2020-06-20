---
title: 취소 옵션(Distributed Replay Administration Tool) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: fea376de-307a-4b45-b7e2-37df88f3681a
author: stevestein
ms.author: sstein
ms.openlocfilehash: d132fbf5ce541a2bdab82e44dc55e6fc92df536d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007752"
---
# <a name="cancel-option-distributed-replay-administration-tool"></a>취소 옵션(Distributed Replay Administration Tool)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 관리 도구인는 `DReplay.exe` Distributed Replay controller와 통신 하는 데 사용할 수 있는 명령줄 도구입니다. 이 항목에서는 **cancel** 명령줄 옵션과 해당 구문에 대해 설명합니다.

 **cancel** 옵션은 컨트롤러에서 실행 중인 현재 작업을 취소합니다.

 ![항목 링크 아이콘](../../database-engine/media/topic-link.gif "항목 링크 아이콘") 관리 도구 구문에서 사용되는 구문 표기 규칙에 대한 자세한 내용은 [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)을 참조하세요.

## <a name="syntax"></a>구문

```

dreplay cancel [-mcontroller] [-q] 
```

#### <a name="parameters"></a>매개 변수
 **-m** *컨트롤러* 컨트롤러의 컴퓨터 이름입니다. "`localhost`" 또는 "`.`"을 사용하여 로컬 컴퓨터를 참조할 수 있습니다.

 **-m** 매개 변수를 지정하지 않으면 로컬 컴퓨터가 사용됩니다.

 **-q** 자동 모드. 확인 메시지를 표시하지 않습니다.

 **-q** 매개 변수는 선택적입니다.

## <a name="examples"></a>예
 다음 예에서는 취소 요청이 자동 모드로 전송됩니다. `localhost` 값은 컨트롤러 서비스가 관리 도구와 동일한 컴퓨터에서 실행 중임을 나타냅니다.

```
dreplay cancel -m localhost -q
```

## <a name="permissions"></a>사용 권한
 관리 도구는 로컬 사용자 또는 도메인 사용자 등의 대화형 사용자 계정으로 실행해야 합니다. 로컬 사용자 계정을 사용하려면 관리 도구와 컨트롤러가 동일한 컴퓨터에서 실행되고 있어야 합니다.

 자세한 내용은 [Distributed Replay Security](distributed-replay-security.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)


