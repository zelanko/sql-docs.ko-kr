---
description: 로컬 실행과 원격 실행의 차이점 이해
title: 로컬 실행과 원격 실행의 차이점 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e9ed7d79855fdef0dfc64d37367ee7b8bc919ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495528"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>로컬 실행과 원격 실행의 차이점 이해

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  패키지 개발자와 관리자는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지가 실행되는 위치와 관련된 제한 사항을 알고 있어야 합니다.  
  
-   **패키지는 해당 패키지를 실행하는 프로그램과 동일한 컴퓨터에서 실행됩니다**. 프로그램에서 다른 서버에 원격으로 저장된 패키지를 로드하더라도 해당 패키지는 로컬 컴퓨터에서 실행됩니다.  
  
-   **Integration Services가 설치된 컴퓨터의 개발 환경 외부에서만 패키지를 실행할 수 있습니다**. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]가 설치되지 않은 클라이언트 컴퓨터의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 외부에서는 패키지를 실행할 수 없으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용권 계약에 따라 추가 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하는 것이 허용되지 않을 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 서버 구성 요소이며 클라이언트 컴퓨터에 재배포할 수 없습니다. 클라이언트 컴퓨터에서 패키지를 실행하려면 패키지가 서버에서 실행되도록 하는 방식으로 실행해야 합니다.  
  
 저장된 패키지를 로드 및 실행하는 방법은 다음을 참조하십시오.  
  
-   [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [프로그래밍 방식으로 원격 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 패키지를 실행하고 해당 출력을 사용자 지정 프로그램으로 로드하는 방법은 다음을 참조하십시오.  
  
-   [로컬 패키지의 출력 로드](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [프로그래밍 방식으로 원격 패키지 로드 및 실행](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [로컬 패키지의 출력 로드](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
