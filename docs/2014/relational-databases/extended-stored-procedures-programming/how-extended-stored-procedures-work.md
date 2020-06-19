---
title: 확장 저장 프로시저의 작동 방식 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 75082fed6b70c214b4f55b85034ffa371824d24f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027129"
---
# <a name="how-extended-stored-procedures-work"></a>확장 저장 프로시저 작동 원리
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저가 작동하는 프로세스는 다음과 같습니다.  
  
1.  클라이언트에서 확장 저장 프로시저를 실행 하면 요청이 TDS (tabular data stream) 또는 SOAP (Simple Object Access Protocol) 형식으로 클라이언트 응용 프로그램에서로 전송 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 확장 저장 프로시저와 연결된 DLL을 검색하고 아직 로드되지 않은 경우 DLL을 로드합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 요청된 확장 저장 프로시저(DLL 내에 함수로 구현됨)를 호출합니다.  
  
4.  확장 저장 프로시저가 결과 집합을 전달하고 확장 저장 프로시저 API를 통해 매개 변수를 서버로 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 확장 저장 프로시저 프로그래밍](../database-engine-extended-stored-procedure-programming.md)  
  
  
