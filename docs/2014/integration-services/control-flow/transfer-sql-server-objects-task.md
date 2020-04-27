---
title: SQL Server 개체 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjectstask.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01b985a1bb818e7b3d3612596bb4e2b7fa6fd393
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62829466"
---
# <a name="transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 한 가지 이상 유형의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 개체를 전송합니다. 예를 들어 이 태스크로 테이블 및 저장 프로시저를 복사할 수 있습니다. 원본으로 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 복사할 수 있는 개체 유형이 달라집니다. 예를 들어 스키마 및 사용자 정의 집계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에만 포함됩니다.  
  
## <a name="objects-to-transfer"></a>전송할 개체  
 전송되는 개체에 대한 사용 권한과 함께 지정된 데이터베이스의 서버 역할, 역할 및 사용자를 복사할 수 있습니다. 개체와 관련된 사용자, 역할 및 사용 권한을 복사하면 전송되는 개체를 대상 서버에서 즉시 작동할 수 있습니다.  
  
 다음 표에서는 복사할 수 있는 개체 유형을 나열합니다.  
  
|Object|  
|------------|  
|테이블|  
|뷰|  
|저장 프로시저|  
|사용자 정의 함수|  
|기본값|  
|사용자 정의 데이터 형식|  
|파티션 함수|  
|파티션 구성표|  
|스키마|  
|어셈블리|  
|사용자 정의 집계|  
|사용자 정의 형식|  
|XML 스키마 컬렉션|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 생성된 UDT(사용자 정의 형식)은 CLR(공용 언어 런타임) 어셈블리에 종속됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 기능을 사용하여 UDT를 전송할 경우 종속 개체를 전송하도록 태스크를 구성해야 합니다. 종속 개체를 전송하려면 `IncludeDependentObjects` 속성을 `True`로 설정합니다.  
  
### <a name="table-options"></a>테이블 옵션  
 테이블을 복사하는 경우 복사 작업에 포함시킬 테이블 관련 항목의 유형을 지정할 수 있습니다. 다음 유형의 항목을 관련 테이블과 함께 복사할 수 있습니다.  
  
-   인덱스  
  
-   트리거  
  
-   전체 텍스트 인덱스  
  
-   기본 키  
  
-   외래 키  
  
 태스크가 생성하는 스크립트가 유니코드 형식인지도 지정할 수 있습니다.  
  
## <a name="destination-options"></a>대상 옵션  
 전송할 때 스키마 이름, 데이터, 전송되는 개체의 확장 속성 및 종속 개체를 포함하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 구성할 수 있습니다. 데이터를 복사할 때는 기존 데이터를 교체 또는 추가할 수 있습니다.  
  
 일부 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에만 적용됩니다. 예를 들어 스키마는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서만 지원됩니다.  
  
## <a name="security-options"></a>보안 옵션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에는 원본의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 수준 사용자 및 역할, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 전송되는 개체에 대한 사용 권한을 포함시킬 수 있습니다. 예를 들어 전송되는 테이블에 대한 사용 권한을 전송에 포함시킬 수 있습니다.  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>SQL Server 인스턴스 간 개체 전송  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 및 대상을 지원합니다.  
  
## <a name="events"></a>이벤트  
 태스크는 전송되는 개체에 대해 보고하는 정보 이벤트를 발생시키며 개체를 덮어쓰는 경우 경고 이벤트를 발생시킵니다. 데이터베이스 테이블 잘림과 같은 동작에서도 정보 이벤트가 발생합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 개체를 전송하는 진행 과정은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 태스크의 `ExecutionValue` 속성에 저장된 실행 값은 전송된 개체 수를 반환합니다. SQL Server 개체 전송 태스크의 `ExecValueVariable` 속성에 사용자 정의 변수를 할당하면 패키지의 다른 개체에서 개체 전송에 대한 정보를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 SQL Server 개체 전송 태스크에는 다음 사용자 지정 로그 항목이 포함됩니다.  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   이 로그 항목에서는 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    이 로그 항목에서는 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 또한 `OnInformation` 이벤트에 대한 로그 항목에서는 전송하도록 선택한 개체 유형의 개체 수, 전송된 개체의 수 및 테이블로 데이터 전송 시 테이블 잘림과 같은 동작을 보고합니다. 대상에서 덮어쓴 개체마다 `OnWarning` 이벤트에 대한 로그 항목이 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 사용자는 원본 서버에서 개체를 검색하는 권한 및 대상 서버에서 개체를 삭제하고 만드는 권한이 필요하며 무엇보다도 지정된 데이터베이스 및 데이터베이스 개체에 대한 액세스가 필요합니다.  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크 구성  
 모든 개체, 한 유형의 모든 개체 또는 한 유형의 지정된 개체만 전송하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 구성할 수 있습니다. 예를 들어 AdventureWorks 데이터베이스에서 선택한 테이블만 복사하도록 선택할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크가 테이블을 전송하는 경우 테이블과 함께 복사할 테이블 관련 개체 유형을 지정할 수 있습니다. 예를 들어 테이블과 함께 복사할 기본 키를 지정할 수 있습니다.  
  
 전송할 때 스키마 이름, 데이터, 전송된 개체의 확장 속성 및 종속 개체를 포함하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크를 구성하여 전송되는 개체의 기능을 더욱 향상시킬 수 있습니다. 데이터 복사할 때 기존 데이터를 교체할지 또는 추가할지를 지정할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크는 런타임에 두 개의 SMO 연결 관리자를 사용하여 원본 서버 및 대상 서버에 연결합니다. SMO 연결 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크와 별도로 구성된 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [SQL Server 개체 전송 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [SQL Server 개체 전송 태스크 편집기&#40;개체 페이지&#41;](../transfer-sql-server-objects-task-editor-objects-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>SQL Server 개체 전송 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
