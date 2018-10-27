---
title: 트랜잭션 관리 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, transactions
- XMLA, transactions
- explicit transactions [XMLA]
- implicit transactions
- transactions [XML for Analysis]
- rolling back transactions, XMLA
- reference counts [XML for Analysis]
- committing transactions
- starting transactions
ms.assetid: f5112e01-82f8-4870-bfb7-caa00182c999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2c9bb93b30b7c2b080c3770e71552d5882ae61d2
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148348"
---
# <a name="managing-transactions-xmla"></a>트랜잭션 관리(XMLA)
  모든 XML for Analysis (XMLA) 명령의 인스턴스로 보낸 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 현재 암시적 또는 명시적 세션의 트랜잭션 컨텍스트 내에서 실행 됩니다. 이러한 트랜잭션을 각각 관리 하려면 사용 합니다 [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)를 [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla), 및 [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) 명령입니다. 이러한 명령을 사용하여 암시적 또는 명시적 트랜잭션을 만들거나 트랜잭션 참조 횟수를 변경하거나 트랜잭션을 시작, 커밋 또는 롤백할 수 있습니다.  
  
## <a name="implicit-and-explicit-transactions"></a>암시적 트랜잭션 및 명시적 트랜잭션  
 트랜잭션은 암시적이거나 명시적입니다.  
  
 **암시적 트랜잭션**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 만듭니다는 *암시적* XMLA에 대 한 트랜잭션을 명령는 `BeginTransaction` 명령 트랜잭션 시작이 지정 되지 않습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 명령이 성공하는 경우 항상 암시적 트랜잭션을 커밋하고 명령이 실패하는 경우 암시적 트랜잭션을 롤백합니다.  
  
 **명시적 트랜잭션**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 만듭니다는 *명시적* 트랜잭션 경우는 `BeginTransaction` 명령에서 트랜잭션을 시작 합니다. 그러나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 `CommitTransaction` 명령이 전송된 경우에만 명시적 트랜잭션을 커밋하고 `RollbackTransaction` 명령이 전송된 경우에는 명시적 트랜잭션을 롤백합니다.  
  
 또한 활성 트랜잭션이 완료되기 전에 현재 세션이 끝나면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 암시적 트랜잭션과 명시적 트랜잭션을 모두 롤백합니다.  
  
## <a name="transactions-and-reference-counts"></a>트랜잭션 및 참조 횟수  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 각 세션의 트랜잭션 참조 횟수를 유지 관리합니다. 그러나 세션별로 하나의 활성 트랜잭션만 유지 관리되는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 중첩된 트랜잭션을 지원하지 않습니다. 현재 세션에 활성 트랜잭션이 없는 경우 트랜잭션 참조 횟수가 0으로 설정됩니다.  
  
 즉, 각 `BeginTransaction` 명령은 참조 횟수를 1씩 늘리고 각 `CommitTransaction` 명령은 참조 횟수를 1씩 줄입니다. `CommitTransaction` 명령에서 트랜잭션 횟수를 0으로 설정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 트랜잭션을 커밋합니다.  
  
 그러나 `RollbackTransaction` 명령은 현재 트랜잭션 참조 횟수 값에 관계없이 활성 트랜잭션을 롤백합니다. 즉, 단일 `RollbackTransaction` 명령은 `BeginTransaction` 명령 또는 `CommitTransaction` 명령을 보낸 횟수에 관계없이 활성 트랜잭션을 롤백하며, 트랜잭션 참조 횟수를 0으로 설정합니다.  
  
## <a name="beginning-a-transaction"></a>트랜잭션 시작  
 `BeginTransaction` 명령은 현재 세션에서 명시적 트랜잭션을 시작하고 현재 세션의 트랜잭션 참조 횟수를 1씩 늘립니다. 이후의 모든 명령은 충분한 `CommitTransaction` 명령을 보내 활성 트랜잭션을 커밋하거나 단일 `RollbackTransaction` 명령을 보내 활성 트랜잭션을 롤백할 때까지 활성 트랜잭션 내에 있는 것으로 간주됩니다.  
  
## <a name="committing-a-transaction"></a>트랜잭션 커밋  
 `CommitTransaction` 명령은 `BeginTransaction` 명령이 현재 세션에서 실행된 후 실행되는 명령 결과를 커밋합니다. 각 `CommitTransaction` 명령은 세션의 활성 트랜잭션 참조 횟수를 줄입니다. `CommitTransaction` 명령이 참조 횟수를 0으로 설정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 활성 트랜잭션을 커밋합니다. 활성 트랜잭션이 없는 경우, 즉 현재 세션의 트랜잭션 참조 횟수가 이미 0으로 설정되어 있는 경우에는 `CommitTransaction` 명령에서 오류가 발생합니다.  
  
## <a name="rolling-back-a-transaction"></a>트랜잭션 롤백  
 `RollbackTransaction` 명령은 현재 세션에서 `BeginTransaction` 명령이 실행된 후 수행되는 명령 결과를 롤백합니다. `RollbackTransaction` 명령은 현재 트랜잭션 참조 횟수에 관계없이 활성 트랜잭션을 롤백하고 트랜잭션 참조 횟수를 0으로 설정합니다. 활성 트랜잭션이 없는 경우, 즉 현재 세션의 트랜잭션 참조 횟수가 이미 0으로 설정되어 있는 경우에는 `RollbackTransaction` 명령에서 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
