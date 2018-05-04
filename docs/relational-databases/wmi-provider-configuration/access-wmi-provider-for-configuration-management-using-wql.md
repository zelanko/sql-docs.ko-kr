---
title: WQL을 사용 하 여 구성 관리용 WMI 공급자 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: 16
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1c12449103010f14ff9466a28543b0c59c979c88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>WQL을 사용하여 구성 관리용 WMI 공급자 액세스
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 섹션에서는 컴퓨터 관리용 WMI 공급자에 대해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] WQL(Windows Management Instrumentation Query Language) 문을 실행하는 방법을 설명합니다.  
  
 이 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 네트워크 프로토콜 및 별칭을 열거하기 위해 WQL 편집기인 WBEMtest.exe를 사용하여 WMI 공급자에 대해 WQL 쿼리를 실행합니다.  
  
### <a name="querying-services-using-wbemtest"></a>WBEMtest를 사용하여 서비스 쿼리  
  
1.  **시작** 메뉴를 클릭 하 여 **실행**, 다음을 입력 하 고 **WBEMtest**합니다.  
  
2.  WBEMtest.exe 대화 상자가 나타납니다. **연결**을 클릭합니다.  
  
3.  첫 번째 텍스트 필드에 컴퓨터 관리용 WMI 공급자 네임스페이스인 root\Microsoft\SqlServer\ComputerManagement11을 입력합니다. **연결**을 클릭합니다.  
  
4.  클릭 **쿼리**합니다. 로컬 컴퓨터에서 실행 중인 현재 서비스를 반환 하는 쿼리를 입력: **선택 \* 에서 SqlService 합니다.** **적용**을 클릭합니다.  
  
5.  추가 하 여 쿼리를 구체화 **여기서 ServiceName = "MSSQLSERVER"** 합니다.  
  
  
