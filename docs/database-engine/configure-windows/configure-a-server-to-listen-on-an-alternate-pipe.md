---
title: "대체 파이프에서 수신 대기하도록 서버 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
caps.latest.revision: "29"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: edc73b858a08ea0f8bda9e7a4d5ede8d2c05cccf
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe"></a>대체 파이프에서 수신 대기하도록 서버 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 대체 파이프로 수신하도록 서버를 구성하는 방법에 대해 설명합니다. 기본적으로 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 기본 인스턴스는 명명된 파이프 \\\\.\pipe\sql\query에서 수신합니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 및 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 의 명명된 인스턴스는 다른 파이프에서 수신합니다.  
  
 클라이언트 응용 프로그램을 사용하여 특정한 명명된 파이프에 연결하는 방법에는 다음 3가지가 있습니다.  
  
-   서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 실행합니다.  
  
-   클라이언트에서 별칭을 만들어 명명된 파이프를 지정합니다.  
  
-   클라이언트가 사용자 지정 연결 문자열을 사용하여 연결하도록 프로그래밍합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진에서 사용하는 명명된 파이프를 구성하려면  
  
1.  SQL Server 구성 관리자의 콘솔 창에서 **SQL Server 네트워크 구성**을 펼친 다음 *\<인스턴스 이름>***에 대한 프로토콜**을 클릭하여 펼칩니다.  
  
2.  세부 정보 창에서 **명명된 파이프**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **프로토콜** 탭의 **파이프 이름** 입력란에 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 수신하도록 할 파이프를 입력한 다음 **확인**을 클릭합니다.  
  
4.  콘솔 창에서 **SQL Server 서비스**를 클릭합니다.  
  
5.  세부 정보 창에서 **SQL Server(**\<인스턴스 이름>**)**를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지하고 다시 시작합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 대체 파이프에서 수신하는 경우 클라이언트 응용 프로그램을 사용하여 특정한 명명된 파이프에 연결하는 방법은 다음 세 가지가 있습니다.  
  
-   서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 실행합니다.  
  
-   클라이언트에서 별칭을 만들어 명명된 파이프를 지정합니다.  
  
-   클라이언트가 사용자 지정 연결 문자열을 사용하여 연결하도록 프로그래밍합니다.  
  
## <a name="see-also"></a>참고 항목  
 [클라이언트에서 사용할 서버 별칭 만들기 또는 삭제&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [서버 네트워크 구성](../../database-engine/configure-windows/server-network-configuration.md)  
  
  
