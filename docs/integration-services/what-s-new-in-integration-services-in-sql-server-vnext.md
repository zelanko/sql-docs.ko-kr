---
title: "SQL Server vNext Integration Services의 새로운 기능 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 3
---
# SQL Server vNext Integration Services의 새로운 기능
이 항목에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 추가되거나 업데이트된 기능에 대해 설명합니다.

>   [!NOTE] SQL Server vNext에는 SQL Server 2016의 기능과 SQL Server 2016 업데이트에서 추가된 기능도 포함되어 있습니다. SQL Server 2016의 새로운 SSIS기능에 대한 자세한 내용은 [SQL Server 2016 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)을 참조하세요.

## <a name="new-in-ssis-in-sql-server-vnext-ctp-11"></a>SQL Server vNext CTP 1.1 SSIS의 새로운 기능

SQL Server vNext CTP 1.1에는 새로운 SSIS 기능이 없습니다.

## <a name="new-in-ssis-in-sql-server-vnext-ctp-10"></a>SQL Server vNext CTP 1.0 SSIS의 새로운 기능

### <a name="scale-out-for-ssis"></a>SSIS용 규모 확장

규모 확장 기능을 사용하면 여러 컴퓨터에서 훨씬 더 쉽게 [!INCLUDE[ssIS_md](../includes/ssis-md.md)]를 실행할 수 있습니다. 
   
규모 확장 마스터 및 작업자를 설치한 후 패키지를 배포하여 다른 작업자에서 자동으로 실행할 수 있습니다. 실행이 예기치 않게 종료되는 경우 실행이 자동으로 다시 시도됩니다. 또한 모든 실행 및 작업자는 마스터를 사용하여 중앙에서 관리할 수 있습니다.
   
자세한 내용은 [Integration Services 규모 확장](../integration-services/integration-services-ssis-scale-out.md)을 참조하세요.
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics Online 리소스 지원

이제 OData 원본 및 OData 연결 관리자가 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결할 수 있습니다.
