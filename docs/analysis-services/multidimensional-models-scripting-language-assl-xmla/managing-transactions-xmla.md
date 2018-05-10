---
title: 트랜잭션 관리 (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d34410453fea22927b36ed7791830f170a0a3a09
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="managing-transactions-xmla"></a>트랜잭션 관리(XMLA)
  인스턴스로 보낸 Analysis (XMLA) 명령에 대 한 모든 XML [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 현재 암시적 또는 명시적 세션에서 트랜잭션 컨텍스트 내에서 실행 됩니다. 이러한 트랜잭션을 각각 관리 하려면 사용 된 [BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), 및 [RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md) 명령입니다. 이러한 명령을 사용하여 암시적 또는 명시적 트랜잭션을 만들거나 트랜잭션 참조 횟수를 변경하거나 트랜잭션을 시작, 커밋 또는 롤백할 수 있습니다.  
  
## <a name="implicit-and-explicit-transactions"></a>암시적 트랜잭션 및 명시적 트랜잭션  
 트랜잭션은 암시적이거나 명시적입니다.  
  
 **암시적 트랜잭션**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 만듭니다는 *암시적* XMLA에 대 한 트랜잭션을 경우 명령에서 **BeginTransaction** 명령은 트랜잭션 시작을 지정 하지 않습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 명령이 성공하는 경우 항상 암시적 트랜잭션을 커밋하고 명령이 실패하는 경우 암시적 트랜잭션을 롤백합니다.  
  
 **명시적 트랜잭션**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 만듭니다는 *명시적* 트랜잭션 하는 경우는 **BeginTransaction** 명령에서 트랜잭션을 시작 합니다. 그러나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 경우에 명시적 트랜잭션을 커밋하는 **CommitTransaction** 명령을 전송 되 고 경우 명시적 트랜잭션을 롤백합니다는 **RollbackTransaction** 명령이 전송 됩니다.  
  
 또한 활성 트랜잭션이 완료되기 전에 현재 세션이 끝나면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 암시적 트랜잭션과 명시적 트랜잭션을 모두 롤백합니다.  
  
## <a name="transactions-and-reference-counts"></a>트랜잭션 및 참조 횟수  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 각 세션의 트랜잭션 참조 횟수를 유지 관리합니다. 그러나 세션별로 하나의 활성 트랜잭션만 유지 관리되는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 중첩된 트랜잭션을 지원하지 않습니다. 현재 세션에 활성 트랜잭션이 없는 경우 트랜잭션 참조 횟수가 0으로 설정됩니다.  
  
 즉, 각 **BeginTransaction** 명령은 참조 횟수를 1 씩 늘리고 각 **CommitTransaction** 씩 참조 횟수를 명령 감소 합니다. 경우는 **CommitTransaction** 트랜잭션 개수를 0으로 설정 하는 명령 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 트랜잭션을 커밋합니다.  
  
 그러나는 **RollbackTransaction** 명령은 트랜잭션 참조 횟수의 현재 값에 관계 없이 활성 트랜잭션을 롤백합니다. 즉, 단일 **RollbackTransaction** 명령은 개수에 관계 없이 활성 트랜잭션을 롤백합니다. **BeginTransaction** 명령 또는 **CommitTransaction** 전송 된 명령과 트랜잭션 참조 횟수를 0으로 설정 합니다.  
  
## <a name="beginning-a-transaction"></a>트랜잭션 시작  
 **BeginTransaction** 명령은 현재 세션에서 명시적 트랜잭션을 시작 하 고 하나에서 현재 세션에 대 한 트랜잭션 참조 횟수를 증가 시킵니다. 이후 모든 명령은 충분 될 때까지 활성 트랜잭션 내 것으로 간주 됩니다 **CommitTransaction** 명령은 단일 또는 활성 트랜잭션 커밋에 전송 되어 **RollbackTransaction**활성 트랜잭션을 롤백할 명령이 전송 됩니다.  
  
## <a name="committing-a-transaction"></a>트랜잭션 커밋  
 **CommitTransaction** 명령 후에 실행 되는 명령 결과 커밋합니다는 **BeginTransaction** 명령이 현재 세션에서 실행 된 합니다. 각 **CommitTransaction** 명령은 참조 횟수를 줄입니다 활성 트랜잭션에 대 한 세션입니다. 경우는 **CommitTransaction** 명령은 참조 횟수를 0으로 설정 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 활성 트랜잭션을 커밋합니다. 활성 트랜잭션이 없는 경우 (즉, 현재 세션의 트랜잭션 참조 횟수는 이미 설정 0)는 **CommitTransaction** 명령에서 오류가 발생 합니다.  
  
## <a name="rolling-back-a-transaction"></a>트랜잭션 롤백  
 **RollbackTransaction** 명령은 후 실행 되는 명령 결과를 롤백합니다.는 **BeginTransaction** 명령이 현재 세션에서 실행 된 합니다. **RollbackTransaction** 명령을 현재 트랜잭션 참조 횟수에 관계 없이 활성 트랜잭션을 롤백하고 트랜잭션 참조 횟수를 0으로 설정 합니다. 활성 트랜잭션이 없는 경우 (즉, 현재 세션의 트랜잭션 참조 횟수는 이미 설정 0)는 **RollbackTransaction** 명령에서 오류가 발생 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
