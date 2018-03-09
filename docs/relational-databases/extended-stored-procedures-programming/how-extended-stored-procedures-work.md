---
title: "확장 저장된 프로시저 작동 원리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb9c6663cd2891669140c7eb59e44e110f3d5607
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="how-extended-stored-procedures-work"></a>확장 저장 프로시저 작동 원리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저가 작동하는 프로세스는 다음과 같습니다.  
  
1.  표 형식 데이터 스트림 (TDS) 또는 클라이언트 응용 프로그램에서 액세스 프로토콜 SOAP (Simple Object) 형식 요청이 전송 되는 클라이언트가 확장된 저장된 프로시저를 실행할 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장된 저장된 프로시저와 관련 된 DLL을 검색 하 고 아직 로드 되지 않은 경우 DLL을 로드 합니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 요청 된 확장 저장된 프로시저 (DLL 내에 함수로 구현 됨).  
  
4.  확장 저장 프로시저가 결과 집합을 전달하고 확장 저장 프로시저 API를 통해 매개 변수를 서버로 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 확장 저장 프로시저 프로그래밍](../../relational-databases/database-engine-extended-stored-procedure-programming.md)  
  
  
