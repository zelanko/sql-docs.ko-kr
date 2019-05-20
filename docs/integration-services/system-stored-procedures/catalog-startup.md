---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e5bec6c25f53da66a4f1d3e6aa09d94b621c81f
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715871"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  SSISDB 카탈로그에 대한 작업의 상태를 유지 관리합니다.  
  
 저장 프로시저는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서버 인스턴스가 다운될 때 실행 중이었던 패키지의 상태를 수정합니다.  
  
 **카탈로그 만들기** 대화 상자에서 **SQL Server 시작 시 Integration Services 저장 프로시저 자동 실행** 옵션을 선택하여 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 서버 인스턴스를 다시 시작할 때마다 저장 프로시저를 자동으로 실행하도록 설정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 및 MODIFY 권한, 프로젝트에 대한 READ 및 EXECUTE 권한, 해당되는 경우 참조된 환경에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
  
