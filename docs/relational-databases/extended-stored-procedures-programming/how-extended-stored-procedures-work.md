---
title: 확장 저장 프로시저의 작동 방식 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 02a1c64974fdcab5a686a61ac35a3a2175e16314
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758087"
---
# <a name="how-extended-stored-procedures-work"></a>확장 저장 프로시저 작동 원리

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저가 작동하는 프로세스는 다음과 같습니다.  
  
1.  클라이언트에서 확장 저장 프로시저를 실행 하면 요청이 TDS (tabular data stream) 또는 SOAP (Simple Object Access Protocol) 형식으로 클라이언트 응용 프로그램에서로 전송 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 확장 저장 프로시저와 연결된 DLL을 검색하고 아직 로드되지 않은 경우 DLL을 로드합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 요청된 확장 저장 프로시저(DLL 내에 함수로 구현됨)를 호출합니다.  
  
4.  확장 저장 프로시저가 결과 집합을 전달하고 확장 저장 프로시저 API를 통해 매개 변수를 서버로 반환합니다.  

