---
title: "SQL Server 데이터베이스 엔진의 인스턴스 숨기기 | Microsoft Docs"
ms.custom: 
ms.date: 08/19/2015
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
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 343740304ad02460baea28da74e65b4298d8c0ba
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진의 인스턴스 숨기기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 숨기는 방법에 대해 설명합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 사용하여 컴퓨터에 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스를 열거합니다. 이렇게 하면 클라이언트 응용 프로그램에서 서버를 검색하고 클라이언트가 같은 컴퓨터에 있는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 여러 인스턴스를 구분할 수 있습니다. 다음 절차를 통해 SQL Server Browser 서비스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 찾아보기 **단추를 사용하여 인스턴스를 찾으려고 하는 클라이언트 컴퓨터에** 인스턴스를 노출하지 않도록 할 수 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>SQL Server 데이터베이스 엔진의 인스턴스를 숨기려면  
  
1.  **SQL Server 구성 관리자**에서 **SQL Server 네트워크 구성**을 펼치고 *\<서버 인스턴스>***에 대한 프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  **플래그** 탭의 **인스턴스 숨기기** 상자에서 **예**를 선택한 다음 **확인** 을 클릭하여 대화 상자를 닫습니다. 변경 내용이 새 연결에 대해 즉시 적용됩니다.  
  
## <a name="remarks"></a>주의  
 명명된 인스턴스를 숨기면 브라우저 서비스가 실행되고 있더라도 숨겨진 인스턴스에 연결할 때 연결 문자열에 포트 번호를 제공해야 합니다. 명명된 숨겨진 인스턴스에 대한 동적 포트 대신 정적 포트를 사용하는 것이 좋습니다.  
  자세한 내용은 [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)을 참조하세요.  
  
### <a name="clustering"></a>Clustering  
 클러스터된 명명된 인스턴스를 숨기면 클러스터 서비스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하지 못할 수도 있습니다. 이렇게 되면 클러스터 인스턴스의 **IsAlive** 검사가 실패하게 되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 오프라인 상태가 됩니다. 인스턴스에 대해 구성한 정적 포트를 반영하도록 클러스터된 인스턴스의 모든 노드에서 별칭을 만드는 것이 좋습니다.  
 자세한 내용은 [클라이언트에서 사용할 서버 별칭 만들기 또는 삭제&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)를 참조하세요.  
  
 클러스터된 명명된 인스턴스를 숨기면 **LastConnect** 레지스트리 키(**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**)에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 수신 중인 포트가 아닌 다른 포트가 있는 경우 클러스터 서비스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하지 못할 수도 있습니다. 클러스터 서비스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 없는 경우 다음과 유사한 오류가 표시될 수 있습니다.  
**Event ID: 1001: Event Name: Failover clustering resource deadlock.**  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 구성](../../database-engine/configure-windows/server-network-configuration.md)   
 [SQL 가상 서버 클라이언트 연결에 대한 설명(영문)](https://support.microsoft.com/kb/273673)   
 [SQL Server라고 명명된 인스턴스에 정적 포트를 할당하고 일반적인 문제를 방지하는 방법(영문)](http://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
