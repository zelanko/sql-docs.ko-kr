---
title: "Integration Services(SSIS) 규모 확장 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Integration Services(SSIS) 규모 확장
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 규모 확장에서는 여러 컴퓨터에 실행을 배포하여 고성능 패키지 실행을 제공합니다. SQL Server Management Studio에서 여러 패키지 실행에 대한 요청을 제출할 수 있습니다. 이러한 패키지는 규모 확장 모드에서 병렬로 실행됩니다.  


## <a name="ssis-scale-out-master-and-scale-out-worker"></a>SSIS 규모 확장 마스터 및 규모 확장 작업자
[!INCLUDE[ssIS_md](../includes/ssis-md.md)] 규모 확장은 하나의 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 규모 확장 마스터와 여러 개의 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 규모 확장 작업자로 구성됩니다. 규모 확장 마스터는 규모 확장 관리를 담당하며 사용자로부터 패키지 실행 요청을 받습니다. 규모 확장 작업자는 규모 확장 마스터에서 실행 작업을 끌어오고 패키지 실행 작업을 수행합니다. 자세한 내용은 [규모 확장 마스터](../integration-services/integration-services-ssis-scale-out-master.md), [규모 확장 작업자](../integration-services/integration-services-ssis-scale-out-worker.md)를 참조하세요.


## <a name="how-to-set-up-scale-out"></a>규모 확장을 설치하는 방법
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 규모 확장은 한 대의 컴퓨터에서 실행되며, 규모 확장 마스터와 규모 확장 작업자는 해당 컴퓨터에 함께 설치됩니다. 또한 규모 확장은 여러 컴퓨터에서 실행되며, 각 규모 확장 작업자는 다른 컴퓨터에 있습니다.
- [연습: Integration Services 규모 확장 설치](../integration-services/walkthrough-set-up-integration-services-scale-out.md)


## <a name="run-packages-in-scale-out"></a>규모 확장에서 패키지 실행
규모 확장은 SSISDB 카탈로그에서 병렬로 여러 패키지 실행을 지원합니다. 자세한 내용은 [규모 확장 시 패키지 실행](../integration-services/run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.

