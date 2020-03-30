---
title: 클라이언트에서 사용할 서버 별칭 만들기 또는 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- server alias
helpviewer_keywords:
- aliases [SQL Server], deleting
- aliases [SQL Server], creating
ms.assetid: b687e376-ee33-470d-b65a-87246bfefe6f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a0a678d3b5df450377517bc9c94d3771c45f22e0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012074"
---
# <a name="create-or-delete-a-server-alias-for-use-by-a-client"></a>클라이언트에서 사용할 서버 별칭 만들기 또는 삭제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 서버 별칭을 만들거나 삭제하는 방법에 대해 설명합니다. 별칭은 연결 설정에 사용할 수 있는 대체 이름입니다. 별칭은 연결 문자열의 필수 요소를 캡슐화하고 사용자가 선택한 이름으로 나타납니다. 별칭은 모든 클라이언트 애플리케이션에서 사용할 수 있습니다. 서버 별칭을 만들면 서버별로 프로토콜과 연결 정보를 지정하지 않아도 클라이언트 컴퓨터가 각기 다른 네트워크 프로토콜을 사용하여 여러 대의 서버에 연결할 수 있습니다. 또한 여러 네트워크 프로토콜을 자주 사용하지 않더라도 이러한 프로토콜을 항상 사용 가능한 상태로 설정할 수 있습니다. 기본값이 아닌 포트 번호나 명명된 파이프에서 수신하도록 서버를 구성하고 SQL Server Browser 서비스를 사용하지 않도록 설정한 경우 새로운 포트 번호나 명명된 파이프를 지정하는 별칭을 만드십시오.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-create-an-alias"></a>별칭을 만들려면  
  
1.  SQL Server 구성 관리자에서 **SQL Server Native Client 구성**을 확장하고 **별칭**을 마우스 오른쪽 단추로 클릭한 다음 **새 별칭**을 클릭합니다.  
  
2.  **별칭** 상자에 별칭 이름을 입력합니다. 클라이언트 애플리케이션은 연결할 때 이 이름을 사용합니다.  
  
3.  **서버** 상자에 서버 이름이나 IP 주소를 입력합니다. 명명된 인스턴트에 인스턴트 이름을 추가합니다.  
  
4.  **프로토콜** 상자에서 이 별칭에 사용되는 프로토콜을 선택합니다. 프로토콜을 선택하면 옵션 속성 상자 제목이 포트 번호, 파이프 이름 또는 연결 문자열로 바뀝니다.  
  
 자신의 연결 문자열을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 도움말에 설명되어 있는 연결 문자열을 참조하면 많은 도움이 될 것입니다. 이 정보에 액세스하려면 **새 별칭** 대화 상자에서 F1을 누르거나 **도움말**을 클릭합니다.  
  
> [!NOTE]  
>  구성된 별칭이 잘못된 서버나 인스턴스에 연결되어 있으면 관련 네트워크 프로토콜을 사용하지 못하게 한 다음 다시 사용 가능하게 하십시오. 그러면 캐시된 연결 정보가 지워지고 클라이언트에서 올바르게 연결할 수 있습니다.  
  
#### <a name="to-delete-an-alias"></a>별칭을 삭제하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server Native Client 구성**을 확장한 다음 **별칭**을 클릭합니다.  
  
2.  세부 정보 창에서 삭제할 별칭을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
  
