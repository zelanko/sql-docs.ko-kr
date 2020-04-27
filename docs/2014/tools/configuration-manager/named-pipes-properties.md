---
title: 명명 된 파이프 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d8b542e709ed7104d851652e75be41ae4d6afec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62911479"
---
# <a name="named-pipes-properties"></a>명명된 파이프 속성
  명명된 파이프 프로토콜을 사용하는 경우 **명명된 파이프 속성** 대화 상자의 **프로토콜** 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수신 대기하는 명명된 파이프를 보거나 변경할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다.  
  
 **파이프 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 수신 대기하는 명명된 파이프를 지정합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 기본 인스턴스의 경우 `\\.\pipe\sql\query` 에서 수신하고, 명명된 인스턴스의 경우 `\\.\pipe\MSSQL$<instancename>\sql\query` 에서 수신합니다. 이 필드는 2047자로 제한됩니다.  
  
## <a name="creating-an-alternate-named-pipe"></a>대체 명명된 파이프 만들기  
 명명된 파이프를 변경하려면 **파이프 이름** 입력란에 새 파이프 이름을 입력한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하고 다시 시작하십시오. **sql\query** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 명명된 파이프로 많이 알려졌으므로 파이프를 변경하면 악의적인 프로그램의 공격 위험을 줄일 수 있습니다.  
  
### <a name="example"></a>예제  
 **\\\\.\pipe\unit\app** 을 입력하여 **unit\app** 파이프를 수신 대기합니다.  
  
 **\\\\.\pipe\acct** 를 입력하여 **acct** 파이프를 수신 대기합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [네트워크 프로토콜 선택](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)  
  
  
