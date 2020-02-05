---
title: CDC를 위해 SQL Server를 준비하는 방법 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f13e8eae235eb040e92baa15247b6094e9aa1075
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294695"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>CDC를 위해 SQL Server를 준비하는 방법

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle CDC Service에서는 모든 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 MSXDBCDC 데이터베이스가 포함되어야 합니다. CDC Service 구성 콘솔에서 SQL Server 준비 동작을 사용하여 이 데이터베이스를 만듭니다. 이 태스크는 각 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 한 번만 수행됩니다.  
  
 다음에서는 CDC Service 구성 콘솔을 사용하여 Oracle Change Data Capture를 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 준비하는 방법에 대해 설명합니다. 이 프로세스는 MSXDBCDC 데이터베이스를 만들고 필수 테이블, 저장 프로시저 및 기타 필수 아티팩트를 정의합니다.  
  
 Oracle CDC를 위해 SQL Server를 준비하는 작업은 Oracle CDC Service 관리자가 수행합니다. CDC Service 관리자 역할에 대한 자세한 내용은 [User Roles](../../integration-services/change-data-capture/user-roles.md)을 참조하십시오.  
  
### <a name="to-enable-sql-server-for-cdc"></a>CDC용 SQL Server를 활성화하려면  
  
1.  **시작** 메뉴에서 **Oracle CDC Service 구성**을 선택합니다.  
  
2.  왼쪽 창에서 **로컬 CDC Service** 를 선택한 다음 **작업** 창에서 **SQL Server 준비**를 클릭합니다.  
  
     **로컬 CDC Service** 를 마우스 오른쪽 단추로 클릭하고 **SQL Server 준비**를 선택할 수도 있습니다.  
  
3.  Oracle CDC를 위한 SQL Server 인스턴스 준비 대화 상자에 필요한 정보를 입력합니다. 이 대화 상자에 필요한 정보를 입력하는 방법은 [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)를 참조하십시오.  
  
     Oracle CDC를 위해 SQL Server 인스턴스를 준비하려면 로그인은 MSXDBCDC 데이터베이스에 대해 쓰기 권한이 있어야 합니다. MSXDBCDC 데이터베이스에 대해 쓰기 권한이 있는 로그인(예: `sysasmin` 역할의 멤버)의 자격 증명을 입력합니다.  
  
 **참고**: **스크립트 보기** 를 클릭하여 설치 스크립트의 읽기 전용 버전을 볼 수 있습니다. 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자는 이 스크립트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 콘솔에 복사하여 편집하고 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC를 위한 SQL Server 준비](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
