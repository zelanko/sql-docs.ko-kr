---
title: 데이터베이스 엔진 구성-사용자 인스턴스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- database engine configuration
- database engine configuration, user instance
ms.assetid: dfc27c1e-0fe2-4221-bed5-f52667ddd3c8
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9f3ec55aa69653667e5f968d0b4368b200431b70
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054951"
---
# <a name="database-engine-configuration---user-instance"></a>데이터베이스 엔진 구성 - 사용자 인스턴스
  **사용자 인스턴스** 페이지를 사용하여 관리자 권한 없이 사용자에 대한 개별 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 생성하고 관리자 역할에 사용자를 추가할 수 있습니다.  
  
## <a name="option"></a>옵션  
 사용자 인스턴스 활성화  
 이 옵션은 기본적으로 사용됩니다. 사용자 인스턴스 활성화 기능을 비활성화하려면 확인란의 선택을 취소하십시오.  
  
 자식 인스턴스 또는 클라이언트 인스턴스라고도 하는 사용자 인스턴스는 부모 인스턴스( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같이 서비스로 실행되는 주 인스턴스)가 사용자 대신 생성하는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]인스턴스입니다. 사용자 인스턴스는 해당 사용자의 보안 컨텍스트에서 사용자 프로세스로 실행됩니다. 사용자 인스턴스는 부모 인스턴스 및 컴퓨터에서 실행되는 그 밖의 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스 기능을 "RANU(일반 사용자로 실행)"라고도 합니다.  
  
> [!NOTE]  
>  설치 중에 **sysadmin** 고정 서버 역할의 멤버로 프로비전되는 로그인은 템플릿 데이터베이스에서 관리자로 프로비전됩니다. 이들은 제거되는 경우가 아니면 사용자 인스턴스에서 **sysadmin** 고정 서버 역할의 멤버가 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 역할에 사용자 추가  
 이 옵션은 기본적으로 사용되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 역할에 현재 설치 사용자를 추가하려면 확인란을 선택하십시오.  
  
 BUILTIN\Administrators의 멤버인 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 사용자는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 연결할 때 sysadmin 고정 서버 역할에 자동으로 추가되지 않습니다. 서버 수준의 관리자 역할에 명시적으로 추가된 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 사용자만 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 관리할 수 있습니다. Built-In\Users 그룹의 멤버는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에 연결할 수 있지만 제한적인 데이터베이스 태스크 수행 권한을 가집니다. 따라서 이전 Windows 릴리스의 BUILTIN\Administrators 및 Built-In\Users에서 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 권한을 상속받은 사용자는 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 에서 실행하는 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]인스턴스에서 관리 권한을 명시적으로 부여 받아야 합니다.  
  
 이 설치 프로그램이 끝난 후 사용자 역할을 변경하려면 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 노출 영역 구성 도구(SQLSAC.exe)를 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 역할의 사용자 목록을 업데이트하려면 **새 관리자 추가** 링크를 클릭합니다.  
  
 **제공할 사용자** 필드에 권한이 업데이트되어야 할 사용자의 DomainName\UserName이 나열되어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 가능한 권한 **창에 있는** 인스턴스 목록에서 업데이트할 역할을 선택한 다음 오른쪽 화살표를 클릭합니다. 사용 가능한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 역할에 사용자를 추가하려면 오른쪽 화살표를 두 번 클릭합니다.  
  
 선택 작업이 완료된 경우 변경 내용을 구현하려면 [!INCLUDE[clickOK](../../includes/clickok-md.md)]. 변경 없이 도구를 끝내려면 **취소**를 클릭합니다.  
  
  
