---
title: Oracle CDC Service 만들기 및 편집 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 10cd612e-d8f1-4af2-97d3-a0c22e1e2326
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7b7db8c28670c4ac411bb2e618f7051d9639fc1
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270388"
---
# <a name="create-and-edit-an-oracle-cdc-service"></a>Oracle CDC Service 만들기 및 편집
  CDC Service 구성 콘솔에서 새 Oracle CDC Windows 서비스를 만들고 편집합니다.  
  
 새 Oracle CDC Windows 서비스를 만들려면 왼쪽 창에서 **로컬 CDC Service** 를 선택한 다음 **동작** 창에서 **새 서비스** 를 클릭합니다. **로컬 CDC Service** 를 마우스 오른쪽 단추로 클릭하고 **새 서비스**를 선택할 수도 있습니다. 새 Oracle CDC Windows 서비스 대화 상자가 열립니다.  
  
 **OR**  
  
 CDC Service 속성을 편집하려면 속성을 편집할 서비스를 선택하고 **동작** 창에서 **속성** 을 클릭합니다. 작업할 서비스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택할 수도 있습니다. CDC Service 속성 대화 상자가 열립니다.  
  
 새 Oracle CDC Windows 서비스 대화 상자 또는 CDC Service 속성 대화 상자에 다음 정보를 입력합니다.  
  
**서비스 이름**  
 새 Oracle CDC Windows 서비스의 이름을 입력합니다. 가급적이면 긴 이름을 사용하지 마십시오. / 및 \ 문자는 서비스 이름에 사용할 수 없습니다.  
  
> [!NOTE]  
> 서비스를 편집하는 경우 이 옵션을 사용할 수 없습니다. 이미 존재하는 Windows 서비스의 이름을 변경할 수 없습니다.  
  
 **설명**  
 식별에 도움이 되도록 서비스에 대한 설명을 입력합니다.  
  
 **서비스 계정**  
 다음 중 하나를 선택하여 서비스를 실행할 계정을 결정합니다.  
  
-   **로컬 시스템 계정**  
  
     이 옵션은 서비스에 너무 많은 권한을 부여하므로 권장되지 않습니다.  
  
-   **계정 지정**  
  
     Windows Vista 또는 Windows Server 2008에서 기본 서비스 계정은 네트워크 서비스 계정입니다.  
  
     Windows 7, Windows Server 2008 R2 이상에서 기본 서비스 계정은 NT Service\\<service-name>입니다.  
  
     이러한 계정에는 암호가 필요 없으므로 이 계정을 사용하면 암호를 사용하지 않고 작업할 수 있습니다. 또한 이러한 계정은 Oracle CDC Service를 실행하는 데 필요한 필수 권한만 제공 합니다.  
  
     로컬 또는 도메인 Windows 계정을 서비스 계정에 사용할 수 있습니다. 이 경우 해당 계정의 **암호** 를 입력해야 합니다. 이 계정은 로컬 호스트 또는 도메인 계정에 사용할 수 있습니다. 암호를 변경할 경우 Windows 제어판에서 로컬 서비스를 사용하여 암호를 업데이트해야 합니다.  
  
 **서버 이름**: 연결할 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택합니다(예: **\\\\<computer_name>\\<instance_name>**). 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
 **인증**  
 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**: 이 옵션을 선택하면 Oracle CDC Service는 서비스 계정 ID를 사용하여 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 다른 컴퓨터에서 실행 중인 경우 도메인 계정과 함께 Windows 인증을 사용해야 합니다.  
  
-   **SQL Server 인증**: 이 옵션을 선택하면 사용하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 **사용자 이름**과 **암호**를 입력해야 합니다. Oracle CDC Service는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때 이러한 자격 증명을 사용합니다.  
  
 Oracle CDC Service에서 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 공용 고정 서버 역할의 구성원이면 가능하며 다른 권한은 필요 없습니다. 새 Oracle CDC 인스턴스를 추가하면 해당 로그인은 연결된 **CDC 데이터베이스에 대한** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 권한을 얻게 됩니다.  
  
 Oracle CDC Windows 서비스 정의를 만들려면 프로그램은 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 MSXDBCDC 데이터베이스에 대한 액세스 권한을 업데이트해야 합니다. **확인**을 클릭하면 사용자가 MSXDBCDC 데이터베이스의 업데이트 권한이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력할 수 있는 대화 상자가 나타납니다.  
  
 SQL Server에 연결 대화 상자에 입력해야 하는 데이터에 대한 자세한 내용은 [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)을 참조하십시오.  
  
 **옵션**  
 화살표를 클릭하면 구성할 수 있는 옵션을 볼 수 있습니다. 이러한 옵션을 기본값으로 그대로 둘 수 있습니다. 사용 가능한 옵션은 다음과 같습니다.  
  
-   **연결 제한 시간**: 제한 시간이 초과되기 전에 Oracle용 CDC Service가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **15**입니다.  
  
-   **실행 제한 시간**: 제한 시간이 초과되기 전에 Oracle CDC Windows 서비스에서 명령이 실행될 때까지 기다리는 시간(초)을 입력합니다. 기본값은 **30**입니다.  
  
-   **연결 암호화**: 암호화된 연결을 사용하는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 Oracle CDC Service 사이의 통신을 위해 **연결 암호화**를 선택합니다.  
  
-   **고급**: 필요한 경우 모든 추가 연결 속성을 입력합니다.  
  
 **마스터 암호**  
 Oracle CDC Windows 서비스에서 Oracle 로그 마이닝 자격 증명을 보호하는 데 사용할 암호를 입력합니다.  
  
 동일한 서비스의 다른 인스턴스가 고가용성 구성에서 한 클러스터의 다른 노드에 대해 구성된 경우에도 동일한 마스터 암호를 사용해야 합니다. 마스터 암호를 잃어버리거나 수정할 경우 CDC Designer 콘솔을 사용하여 Oracle CDC 인스턴스 데이터베이스에 저장된 모든 로그 마이닝 암호를 다시 입력해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC Service를 만들고 편집하는 방법](../../integration-services/change-data-capture/how-to-create-and-edit-a-cdc-service.md)  
  
  
