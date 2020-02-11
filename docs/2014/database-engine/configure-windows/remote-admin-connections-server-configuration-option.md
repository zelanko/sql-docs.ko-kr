---
title: remote admin connections 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4e4894fa7e05c863095fdca7b26f448efe176216
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62781492"
---
# <a name="remote-admin-connections-server-configuration-option"></a>remote admin connections 서버 구성 옵션
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 DAC(관리자 전용 연결)를 제공합니다. DAC를 사용하면 서버가 잠겨 있거나 비정상적인 상태로 작동 중이어서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 연결에 응답하지 않는 경우에도 관리자가 실행 중인 서버에 액세스하여 진단 기능 또는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 문을 실행하거나 서버의 문제를 해결할 수 있습니다. 기본적으로 DAC는 서버의 클라이언트에서만 사용할 수 있습니다. 원격 컴퓨터의 클라이언트 애플리케이션에서 DAC를 사용할 수 있도록 하려면 sp_configure의 remote admin connections 옵션을 사용하십시오.  
  
 기본적으로 DAC는 루프백 IP 주소(127.0.0.1), 포트 1434에서만 수신합니다. TCP 포트 1434를 사용할 수 없는 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 시작되면 TCP 포트가 동적으로 할당됩니다. 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 둘 이상 설치되어 있으면 오류 로그에서 TCP 포트 번호를 확인하십시오.  
  
 다음 표에서는 remote admin connections 옵션에 사용할 수 있는 값을 보여줍니다.  
  
|값|Description|  
|-----------|-----------------|  
|0|DAC를 사용하여 로컬 연결만 허용됨을 나타냅니다.|  
|1|DAC를 사용하여 원격 연결이 허용됨을 나타냅니다.|  
  
## <a name="example"></a>예제  
 다음 예에서는 원격 컴퓨터에서 DAC를 사용합니다.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 관리자를 위한 진단 연결](diagnostic-connection-for-database-administrators.md)  
  
  
