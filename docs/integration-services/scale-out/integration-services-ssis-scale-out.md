---
title: "SQL Server Integration Services (SSIS) 확장 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce7fb96901e8af4da74392fe0a0a85c6e2ec05a4
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out"></a>Integration Services(SSIS) 규모 확장
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 규모 확장에서는 여러 컴퓨터에 실행을 배포하여 고성능 패키지 실행을 제공합니다. SQL Server Management Studio의 여러 패키지 실행에 대 한 요청을 제출할 수 있습니다. 이러한 패키지는 규모 확장 모드에서 병렬로 실행됩니다.  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]범위 확장 구성는 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] 스케일 아웃 마스터 하나 이상의 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] 스케일 아웃 작업자입니다. 규모 확장 마스터는 규모 확장 관리를 담당하며 사용자로부터 패키지 실행 요청을 받습니다. 규모 확장 작업자는 규모 확장 마스터에서 실행 작업을 끌어오고 패키지 실행 작업을 수행합니다. 자세한 내용은 [규모 확장 마스터](integration-services-ssis-scale-out-master.md), [규모 확장 작업자](integration-services-ssis-scale-out-worker.md)를 참조하세요.

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]스케일 아웃 스케일 아웃 마스터 및 스케일 아웃 작업자를 나란히 컴퓨터에 설정 되어 있는 컴퓨터 한 대에서 구성할 수 있습니다. 또한 규모 확장은 여러 컴퓨터에서 실행되며, 각 규모 확장 작업자는 다른 컴퓨터에 있습니다.
- [연습: Integration Services 규모 확장 설치](walkthrough-set-up-integration-services-scale-out.md)

규모 확장은 SSISDB 카탈로그에서 병렬로 여러 패키지 실행을 지원합니다. 자세한 내용은 [규모 확장 시 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.

