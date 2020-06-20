---
title: 배포자 속성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distdbproperties.f1
- sql12.rep.configdistwizard.distproperties.general.f1
- sql12.rep.configdistwizard.distproperties.publishers.f1
- sql12.rep.configdistwizard.distproperties.publishers.f1
ms.assetid: f643c7c3-f238-4835-b81e-2c2b3b53b23f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 501c7931d651498fea49749be38af374c02424ab
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010779"
---
# <a name="sql-server-replication-distributor-properties"></a>SQL Server 복제 배포자 속성
이 항목에서는 **배포자 속성** 창 내에서 **일반**, **게시자**및 **배포 데이터베이스** 페이지에 있는 속성에 대해 설명 합니다. 

## <a name="general"></a>일반
  **배포자 속성** 의 **일반** 페이지에서 배포 데이터베이스를 추가 및 삭제하고 배포 데이터베이스 속성을 설정할 수 있습니다.  
  
 배포 데이터베이스는 모든 유형의 복제에 대한 메타데이터 및 기록 데이터와 트랜잭션 복제에 대한 트랜잭션을 저장합니다. 대부분의 경우 배포 데이터베이스는 하나면 충분합니다. 그러나 여러 게시자가 단일 배포자를 사용하는 경우에는 각 게시자에 대해 배포 데이터베이스를 만들어 보십시오. 이렇게 하면 각 배포 데이터베이스를 통한 데이터 흐름이 고유하게 유지됩니다.  
  
### <a name="options"></a>옵션  
 **데이터베이스**  
 **데이터베이스** 속성 표는 배포자에 있는 배포 데이터베이스의 이름 및 보존 속성을 표시합니다. **트랜잭션 보존** 은 트랜잭션 복제에 대해 트랜잭션을 저장하는 시간입니다. 트랜잭션 보존을 배포 보존이라고도 합니다. **기록 보존** 은 모든 유형의 복제에 대해 기록 메타데이터를 저장하는 시간입니다. 배포 기간에 대한 자세한 내용은 [구독 만료 및 비활성화](subscription-expiration-and-deactivation.md)를 참조하세요.  
  
 **배포 데이터베이스 속성**대화 상자를 시작하려면 **데이터베이스** 속성 표의 속성 단추 ( **...** )를 클릭합니다.  
  
 **새로 만들기**  
 새 배포 데이터베이스를 만들려면 클릭합니다.  
  
 **Delete**  
 **데이터베이스** 속성 표에서 기존 배포 데이터베이스를 선택하고 **삭제** 를 클릭하여 데이터베이스를 삭제합니다. 배포 데이터베이스가 하나만 있는 경우 배포 데이터베이스를 삭제할 수 없습니다. 각 배포자에는 배포 데이터베이스가 최소한 하나 이상 있어야 합니다. 배포 데이터베이스를 모두 삭제하려면 컴퓨터에서 배포를 해제해야 합니다. 자세한 내용은 [게시 및 배포 해제](disable-publishing-and-distribution.md)를 참조하세요.  
  
 **프로필 기본값**  
 **에이전트 프로필** 대화 상자의 복제 에이전트 프로필에 액세스하려면 클릭합니다. 프로필에 대한 자세한 내용은 [Replication Agent Profiles](agents/replication-agent-profiles.md)을 참조하십시오.  

## <a name="publishers"></a>게시자

  **배포자 속성** 대화 상자의 **게시자** 페이지를 사용하여 게시자가 이 배포자를 사용하도록 허용할 수 있습니다. 해당 게시자와 연결된 속성을 설정할 수도 있습니다. 현재 서버를 원격 배포자로 사용하도록 게시자를 설정해도 해당 서버가 게시자가 되지는 않습니다. 게시자에 연결하여 이를 게시자로 구성하고, 이 서버를 배포자로 선택해야 합니다. 새 게시 마법사를 통해 게시자를 구성하고 배포자를 선택할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **게시자**  
 이 배포자를 사용하도록 허용할 서버를 선택합니다. 게시자 옆의 속성 단추 ( **...** )를 클릭하여 추가 속성을 보고 설정할 수 있습니다.  
  
 **추가**  
 허용할 서버가 나열되지 않으면 **추가**를 클릭하여 사용 가능한 게시자 목록에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자 또는 Oracle 게시자를 추가합니다. 추가한 서버가 이 배포자를 원격 배포자로 사용하는 첫 번째 서버이면 관리 연결 암호를 입력하라는 메시지가 표시됩니다.  
  
 **관리 연결 암호**  
 복제에서 **distributor_admin** 로그인을 사용하여 게시자와 원격 배포자 간에 구성하는 연결의 암호를 지정하거나 업데이트하려면 사용합니다.  
  
-   배포자가 로컬 배포자로만 사용되는 경우 이 암호는 임의로 생성되고 자동으로 구성됩니다.  
-   배포자에 원격 게시자가 있으면 이 페이지 또는 배포 구성 마법사의 **배포자 암호** 페이지에서 암호를 이미 입력한 것입니다.    
-   이 배포자에 대해 원격 게시자를 처음으로 설정하는 경우 암호를 입력하라는 메시지가 표시됩니다.  
  
 배포자 보안에 자세한 내용은 [배포자 보안 설정](security/secure-the-distributor.md)을 참조하세요.  

## <a name="distribution-database"></a>배포 데이터베이스
 **배포 데이터베이스 속성** 대화 상자를 사용하여 많은 속성을 보고 데이터베이스의 트랜잭션 보존 기간과 기록 보존 기간을 설정할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **이름**  
 배포 데이터베이스의 이름으로 기본값은 'distribution'입니다(읽기 전용).  
  
 **파일 위치**  
 데이터베이스 파일과 로그 파일의 위치입니다(읽기 전용).  
  
 **트랜잭션 보존 기간**  
 배포 보존 기간이라고도 합니다. 트랜잭션 복제에서 트랜잭션이 저장되는 시간입니다. 자세한 내용은 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)을(를) 참조하세요.  
  
 **기록 보존 기간**  
 모든 복제 유형에서 기록 메타데이터가 저장되는 시간입니다.  
  
 **큐 판독기 에이전트 보안**  
 큐 판독기 에이전트는 지연 업데이트 구독이 있는 트랜잭션 복제에서 사용합니다. 새 게시 마법사의 **게시 유형** 페이지에서 **업데이트할 수 있는 구독이 있는 트랜잭션 게시** 를 선택하면 큐 판독기 에이전트가 자동으로 생성됩니다. **보안 설정...** 을 클릭하여 에이전트를 실행하고 배포자에 연결되는 계정을 변경합니다.  
  
 이 페이지에서 **큐 판독기 에이전트 만들기** 를 선택하여 큐 판독기 에이전트를 만들 수도 있습니다. 에이전트가 이미 생성된 경우에는 이 옵션을 사용할 수 없습니다.  
  
 큐 판독기 에이전트에 대한 추가 연결 정보는 다음 두 위치에서 지정합니다.    
-   에이전트는 **게시자 속성** 대화 상자에서 지정한 자격 증명을 사용하여 게시자에 연결합니다. 이 대화 상자는 **배포자 속성** 대화 상자의 **게시자** 페이지에서 사용할 수 있습니다.    
-   에이전트는 새 구독 마법사에서 배포 에이전트에 대해 지정된 자격 증명을 사용하여 구독자에 연결합니다.  
  
 자세한 내용은 \\ [Replication Agent Security Model](security/replication-agent-security-model.md)을 참조 하세요. 

  
## <a name="see-also"></a>참고 항목  
 [배포 구성](configure-distribution.md)   
 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)   

  
  
