---
title: SSIS(SQL Server Integration Services) Scale Out | Microsoft Docs
description: 이 문서에서는 SSIS 패키지 고성능 실행을 제공하는 SSIS(SQL Server Integration Services) Scale Out 기능을 간략하게 설명
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4b4a5b5f27f959f3a04bb3cf5468d198d3ef5267
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295661"
---
# <a name="integration-services-ssis-scale-out"></a>Integration Services(SSIS) 규모 확장

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
