---
title: WQL을 사용 하 여 WMI 공급자 액세스
description: 이 예제를 사용 하 여 SQL Server에서 컴퓨터 관리용 WMI 공급자에 대해 WMI(Windows Management Instrumentation) 쿼리 언어 문을 실행 하는 방법을 확인할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 27b03d13ede2b861f90e194e4939e8c9c77ecafb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542754"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>WQL을 사용하여 구성 관리용 WMI 공급자 액세스
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 섹션에서는 컴퓨터 관리용 WMI 공급자에 대해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] WQL(Windows Management Instrumentation Query Language) 문을 실행하는 방법을 설명합니다.  
  
 이 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 네트워크 프로토콜 및 별칭을 열거하기 위해 WQL 편집기인 WBEMtest.exe를 사용하여 WMI 공급자에 대해 WQL 쿼리를 실행합니다.  
  
### <a name="querying-services-using-wbemtest"></a>WBEMtest를 사용하여 서비스 쿼리  
  
1.  **시작** 메뉴에서 **실행**을 클릭 한 다음 **WBEMtest**를 입력 합니다.  
  
2.  WBEMtest.exe 대화 상자가 나타납니다. **연결**을 클릭합니다.  
  
3.  첫 번째 텍스트 필드에 컴퓨터 관리용 WMI 공급자 네임스페이스인 root\Microsoft\SqlServer\ComputerManagement11을 입력합니다. **연결**을 클릭합니다.  
  
4.  **쿼리**를 클릭합니다. 로컬 컴퓨터에서 실행 중인 현재 서비스를 반환 하는 쿼리를 입력 ** \* 합니다. Sqlservice에서 선택 합니다.** **적용**을 클릭합니다.  
  
5.  **WHERE ServiceName = "MSSQLSERVER"를**추가 하 여 쿼리를 구체화 합니다.  
  
  
