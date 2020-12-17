---
title: SQL Server Integration Services 속성(서비스 탭)
description: 이진 경로, 호스트 이름, 시작 모드 등 Integration Services 속성 대화 상자의 서비스 탭에 있는 옵션에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 37f0acd9-c96f-48fd-9b53-2ca0097af242
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 2b335440c5f1cf54404f74d8550e5ee687d08307
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463744"
---
# <a name="sql-server-integration-services-properties-service-tab"></a>SQL Server Integration Services 속성(서비스 탭)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] **속성** 대화 상자의 **서비스** 탭을 사용하여 다음 옵션을 확인하거나 지정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **이진 경로**  
 이 서비스에 사용되는 프로그램 파일의 위치를 표시합니다.  
  
 **오류 제어**  
 1은 `SERVICE_ERROR_NORMAL`을 나타냅니다. 컴퓨터 시작 중에 서비스를 시작하지 못하면 시작 프로그램은 오류를 기록하고 팝업 메시지 상자를 표시하지만 컴퓨터를 시작하는 작업은 계속됩니다. 이 값은 변경할 수 없습니다.  
  
 **종료 코드**  
 서비스를 시작하거나 종료할 때 발생하는 모든 문제를 정의하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 오류 코드입니다. 오류가 이 클래스가 나타내는 서비스에 고유한 것이고 **ServiceSpecificExitCode** 속성에서 오류 정보를 사용할 수 있으면 이 속성은 **ERROR_SERVICE_SPECIFIC_ERROR** (1066)로 설정됩니다. 서비스는 실행 중일 때와 정상 종료 시 다시 이 값을 NO_ERROR(0)로 설정합니다.  
  
 **Host Name**  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서비스가 실행되는 컴퓨터 또는 클러스터의 이름을 표시합니다.  
  
 **이름**  
 서비스의 표시 이름을 나타냅니다.  
  
 **프로세스 ID**  
 Windows 프로세스 ID를 표시합니다.  
  
 **SQL 서비스 유형**  
 호출 프로세스에 제공되는 서비스의 유형을 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 몇 가지 서비스를 설치합니다.  
  
 **시작 모드**  
 이 서비스를 다음 옵션으로 설정합니다.  
  
-   수동: 이 서비스는 컴퓨터가 시작될 때 자동으로 시작되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자나 다른 도구를 사용하여 서비스를 시작해야 합니다.  
  
-   자동: 이 서비스는 컴퓨터가 시작될 때 시작됩니다.  
  
-   사용 안 함: 이 서비스를 시작할 수 없습니다.  
  
 **State**  
 이 서비스가 실행 중인지, 중지되었는지 또는 비활성화되었는지 나타냅니다. “ **...** ”는 상태 변경이 보류 중임을 나타냅니다.  
  
  
