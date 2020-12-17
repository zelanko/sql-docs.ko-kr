---
title: 명명된 파이프 속성
description: 명명된 파이프 속성 대화 상자의 프로토콜 페이지를 사용하여 명명된 파이프 프로토콜을 사용할 때 SQL Server에서 수신하는 명명된 파이프를 확인 또는 변경할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: c4929816503430c151c80735078d6a71b0221e71
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463848"
---
# <a name="named-pipes-properties"></a>명명된 파이프 속성
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  명명된 파이프 프로토콜을 사용하는 경우 **명명된 파이프 속성** 대화 상자의 **프로토콜** 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 수신 대기하는 명명된 파이프를 보거나 변경할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 가능한 값은 **예** 및 **아니요** 입니다.  
  
 **파이프 이름**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 수신 대기하는 명명된 파이프를 지정합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 기본 인스턴스의 경우 `\\.\pipe\sql\query` 에서 수신하고, 명명된 인스턴스의 경우 `\\.\pipe\MSSQL$<instancename>\sql\query` 에서 수신합니다. 이 필드는 2047자로 제한됩니다.  
  
## <a name="creating-an-alternate-named-pipe"></a>대체 명명된 파이프 만들기  
 명명된 파이프를 변경하려면 **파이프 이름** 입력란에 새 파이프 이름을 입력한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하고 다시 시작하십시오. **sql\query** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 명명된 파이프로 많이 알려졌으므로 파이프를 변경하면 악의적인 프로그램의 공격 위험을 줄일 수 있습니다.  
  
### <a name="example"></a>예제  
 **\\\\.\pipe\unit\app** 을 입력하여 **unit\app** 파이프를 수신 대기합니다.  
  
 **\\\\.\pipe\acct** 를 입력하여 **acct** 파이프를 수신 대기합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [네트워크 프로토콜 선택](/previous-versions/sql/sql-server-2016/ms187892(v=sql.130))   
 [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](/previous-versions/sql/sql-server-2016/ms189307(v=sql.130))  
  
