---
title: sqlcmd를 사용하여 데이터베이스 엔진에 연결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ea4dda5eb99066bc88e0fde9a1c9b98abaeacf8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227213"
---
# <a name="connect-to-the-database-engine-with-sqlcmd"></a>sqlcmd를 사용하여 데이터베이스 엔진에 연결
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 TCP/IP 네트워크 프로토콜(기본값) 및 명명된 파이프 프로토콜을 통한 클라이언트 통신을 지원합니다. 클라이언트가 동일 컴퓨터의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하고 있는 경우 공유 메모리 프로토콜도 사용할 수 있습니다. 일반적으로 프로토콜을 선택하는 방법에는 3가지가 있습니다. **sqlcmd** 유틸리티에서 사용하는 프로토콜은 다음과 같은 순서로 결정됩니다.  
  
-   **sqlcmd** 는 다음 설명과 같이 연결 문자열의 일부로 지정된 프로토콜을 사용합니다.  
  
-   프로토콜을 연결 문자열의 일부로 지정하지 않으면 **sqlcmd** 는 연결하고 있는 별칭의 일부로 정의된 프로토콜을 사용합니다. 별칭을 만들어 특정 네트워크 프로토콜을 사용하도록 **sqlcmd**를 구성하려면 [클라이언트에서 사용할 서버 별칭 만들기 또는 삭제&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)를 참조하세요.  
  
-   기타 다른 방법으로 프로토콜을 지정하지 않으면 **sqlcmd** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 프로토콜 순서에 따라 결정되는 네트워크 프로토콜을 사용합니다.  
  
 다음 예에서는 포트 1433에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 기본 인스턴스에 연결하고 포트 1691에서 수신하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 명명된 인스턴스에 연결하는 여러 가지 방법을 보여 줍니다. 일부 예에서는 루프백 어댑터의 IP 주소(127.0.0.1)를 사용합니다. 컴퓨터의 네트워크 인터페이스 카드의 IP 주소를 사용하여 테스트합니다.  
  
 인스턴스 이름을 지정하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 IP 주소를 지정하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 TCP\IP 포트 번호를 지정하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>TCP/IP를 사용하여 연결하려면  
  
-   다음 일반 구문을 사용하여 연결합니다.  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   기본 인스턴스에 연결합니다.  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   명명된 인스턴스에 연결합니다.  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>명명된 파이프를 사용하여 연결하려면  
  
-   다음 일반적인 구문 중 하나를 사용하여 연결합니다.  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   기본 인스턴스에 연결합니다.  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   명명된 인스턴스에 연결합니다.  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>서버에 있는 클라이언트에서 공유 메모리(로컬 프로시저 호출)를 사용하여 연결하려면  
  
-   다음 일반적인 구문 중 하나를 사용하여 연결합니다.  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   기본 인스턴스에 연결합니다.  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   명명된 인스턴스에 연결합니다.  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
