---
title: 알 수 없는 서비스 (로그온 탭) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 32b6943792ae89d25709217fe9325d2450aba893
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023779"
---
# <a name="unknown-service-log-on-tab"></a>알 수 없는 서비스(로그온 탭)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자가 이 서비스를 식별할 수 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 서비스가 실행되는 컴퓨터의 WMI 공급자로부터 서비스 정보를 받습니다. 서비스 속성을 읽는 동안 오류가 발생했거나 서비스 속성이 완전하지 않습니다. 이 문제를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 닫은 후 다시 열거나 서비스가 실행되는 컴퓨터의 WMI 공급자를 확인하십시오.  
  
 WMI 공급자는 Windows 구성 요소입니다. WMI 공급자에 대한 사용 권한을 확인하는 방법은 SQL Server 온라인 설명서의 "방법: WMI를 구성하여 SQL Server 도구에 서버 상태 표시"를 참조하세요.  
  
 올바른 서비스가 표시되는 경우 **알 수 없는 서비스 속성** 대화 상자의 **로그온** 탭을 사용하여 이 서비스에서 사용할 계정을 지정할 수 있으며 서비스를 시작 및 중지할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **로컬 시스템 계정**  
 암호를 요구하지 않는 로컬 시스템 계정을 지정합니다. 그러나 로컬 시스템 계정은 계정에 부여된 권한에 따라 서비스가 다른 서버와 상호 작용하지 못하도록 할 수 있습니다.  
  
 **계정 지정**  
 Windows 인증을 사용하는 로컬 또는 도메인 사용자 계정을 지정합니다. 서비스에 대해 최소의 권한을 가진 도메인 사용자 계정을 사용하는 것이 좋습니다. 계정 선택 방법은 SQL Server 온라인 설명서의 "Windows 서비스 계정 설정"을 참조하십시오.  
  
 **계정 이름**  
 로컬 또는 도메인 사용자 계정 이름을 지정합니다.  
  
 **암호**  
 계정의 암호를 입력합니다.  
  
 **암호 확인**  
 계정의 암호를 다시 입력합니다.  
  
 **시작**  
 서비스를 시작합니다.  
  
 **중지**  
 서비스를 중지합니다.  
  
 **일시 중지**  
 서비스를 일시 중지합니다.  
  
 **재개**  
 일시 중지한 서비스를 다시 시작합니다.  
  
  
