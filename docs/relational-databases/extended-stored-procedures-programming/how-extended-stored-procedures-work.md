---
title: 확장 저장된 프로시저 작동 원리 | Microsoft Docs
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
ms.openlocfilehash: 3c9b8bf0da73545a9ec9c582aedf5b8f44980c5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064335"
---
# <a name="how-extended-stored-procedures-work"></a>확장 저장 프로시저 작동 원리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저가 작동하는 프로세스는 다음과 같습니다.  
  
1.  요청 표 형식 데이터 스트림 (TDS) 또는 클라이언트 응용 프로그램에서 액세스 프로토콜 SOAP (Simple Object) 형식으로 전송 되는 클라이언트는 확장된 저장된 프로시저를 실행할 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 확장 저장 프로시저와 연결된 DLL을 검색하고 아직 로드되지 않은 경우 DLL을 로드합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 요청된 확장 저장 프로시저(DLL 내에 함수로 구현됨)를 호출합니다.  
  
4.  확장 저장 프로시저가 결과 집합을 전달하고 확장 저장 프로시저 API를 통해 매개 변수를 서버로 반환합니다.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

