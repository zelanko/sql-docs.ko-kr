---
title: SQL Server Compact Edition 대상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5aa77d90f34a299509acdeab73be6efadd452914
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-compact-edition-destination"></a>SQL Server Compact Edition 대상
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터베이스에 데이터를 기록합니다.  
  
> [!NOTE]  
>  64비트 컴퓨터에서는 32비트 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 데이터 원본에 연결하는 패키지를 실행해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 데이터 원본에 연결할 때 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 공급자는 32비트 버전에서만 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상을 구성할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상에서 데이터를 삽입하는 테이블의 이름을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상의 사용자 지정 속성인 TableName에는 테이블 이름이 포함됩니다.  
  
 이 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 연결 관리자를 사용하여 데이터 원본에 연결하며 연결 관리자에서는 사용할 OLE DB 공급자를 지정합니다. 자세한 내용은 [SQL Server Compact Edition 연결 관리자](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)를 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상은 패키지 로드 시 속성 식을 사용하여 업데이트할 수 있는 TableName 사용자 지정 속성을 포함합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md), [패키지에서 속성 식 사용](../../integration-services/expressions/use-property-expressions-in-packages.md) 및 [SQL Server Compact Edition 대상 사용자 지정 속성](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 대상에는 하나의 입력이 있으며 오류 출력은 지원하지 않습니다.  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>SQL Server Compact Edition 대상 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [SQL Server 대상 사용자 지정 속성](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>관련 작업  
 이 구성 요소의 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름](../../integration-services/data-flow/data-flow.md)  
  
  
