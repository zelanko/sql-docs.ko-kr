---
title: SQL Server Browser 속성(서비스 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 98ace9b0-72d5-4b72-9b7b-11fbc490981a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6421b0a7d6703e2a5d126aa83b227166492558a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211154"
---
# <a name="sql-server-browser-properties-service-tab"></a>SQL Server Browser 속성(서비스 탭)
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 프로그램은 서버에서 서비스로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser는 리소스에 대해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 들어오는 요청을 수신 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 설치 된 인스턴스에 대 한 정보를 제공 합니다.  
  
 
  **SQL Server Browser 속성** 대화 상자의 **서비스** 탭을 사용하여 다음 옵션을 확인할 수 있습니다. 
  **시작 모드** 를 제외한 모든 속성은 읽기 전용입니다.  
  
## <a name="options"></a>옵션  
 **이진 경로**  
 이 서비스에 사용되는 프로그램 파일의 위치를 표시합니다.  
  
 **오류 제어**  
 1은 `SERVICE_ERROR_NORMAL`을 나타냅니다. 컴퓨터 시작 중에 서비스를 시작하지 못하면 시작 프로그램은 오류를 기록하고 팝업 메시지 상자를 표시하지만 컴퓨터를 시작하는 작업은 계속됩니다. 이 값은 변경할 수 없습니다.  
  
 **종료 코드**  
 오류가 발생하면 이 상자에 오류 번호가 나타납니다. 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료에서 이 번호를 검색하여 오류를 해결하거나 기술 지원부에 이 번호를 제공하십시오.  
  
 **호스트 이름**  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 실행되는 컴퓨터 또는 클러스터의 이름을 표시합니다.  
  
 **이름**  
 서비스의 표시 이름을 나타냅니다.  
  
 **프로세스 ID**  
 Windows 프로세스 ID를 표시합니다.  
  
 **서비스 유형**  
 호출 프로세스에 제공되는 서비스의 유형을 표시합니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 몇 가지 서비스를 설치합니다.  
  
 **시작 모드**  
 이 서비스를 다음 옵션으로 설정합니다.  
  
-   수동: 컴퓨터가 시작될 때 이 서비스가 자동으로 시작되지 않습니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자나 다른 도구를 사용하여 서비스를 시작해야 합니다.  
  
-   자동: 컴퓨터가 시작될 때 이 서비스가 시작됩니다.  
  
-   사용 안 함: 이 서비스를 시작할 수 없습니다.  
  
 **시스템 상태**  
 이 서비스가 실행 중인지, 중지되었는지 또는 비활성화되었는지 나타냅니다. “**...**”는 상태 변경이 보류 중임을 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Browser 서비스](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
