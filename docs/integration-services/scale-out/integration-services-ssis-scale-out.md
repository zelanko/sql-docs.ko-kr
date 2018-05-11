---
title: SSIS(SQL Server Integration Services) Scale Out | Microsoft Docs
ms.description: This article provides an overview of the SQL Server Integration Services (SSIS) Scale Out feature, which provides high-performance execution of SSIS packages
ms.custom: ''
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 14f02912f300cfa6b45d38aa95c0d66235aea324
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-ssis-scale-out"></a>Integration Services(SSIS) 규모 확장
SSIS(SQL Server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) Scale Out에서는 여러 컴퓨터에 패키지 실행을 배포하여 SSIS 패키지의 고성능 실행을 제공합니다. Scale Out을 설정한 후에 SSMS(SQL Server Management Studio)에서 스케일 아웃 모드로 동시에 여러 패키지를 실행할 수 있습니다.

## <a name="components"></a>구성 요소
[!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out은 하나의 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 마스터와 여러 개의 [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out 작업자로 구성됩니다.

-   규모 확장 마스터는 규모 확장 관리를 담당하며 사용자로부터 패키지 실행 요청을 받습니다. 자세한 내용은 [Scale Out 마스터](integration-services-ssis-scale-out-master.md)를 참조하세요.

-   Scale Out 작업자는 Scale Out 마스터에서 실행 작업을 끌어오고 패키지를 실행합니다. 자세한 내용은 [Scale Out 작업자](integration-services-ssis-scale-out-worker.md)를 참조하세요.

## <a name="configuration-options"></a>구성 옵션
다음과 같은 구성으로 Scale Out을 설정할 수 있습니다.

-   **단일 컴퓨터에서** 여기서는 Scale Out 마스터 및 Scale Out 작업자를 같은 컴퓨터에서 나란히 실행합니다.

-   **여러 컴퓨터에서** 여기서는 다른 컴퓨터에 각 Scale Out 작업자가 배치됩니다.

## <a name="what-you-can-do"></a>수행 가능한 작업
Scale Out을 설정한 후에 다음과 같은 작업을 수행할 수 있습니다.

-   동시에 SSISDB 카탈로그에 배포된 여러 패키지를 실행합니다. 자세한 내용은 [Scale Out으로 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.

-   Scale Out 관리자 앱에서 Scale Out 토폴로지를 관리합니다. 자세한 내용은 [Integration Services Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계
-   [단일 컴퓨터에서 Integration Services(SSIS) Scale Out 시작](get-started-with-ssis-scale-out-onebox.md)

-   [연습: Integration Services 규모 확장 설치](walkthrough-set-up-integration-services-scale-out.md)
